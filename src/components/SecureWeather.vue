<template>
   
    <div class="main-container">    
     <div class="phone">
        <div class="circle-container">
            <div class="circle">
                <div class="inner-circle"></div>
            </div>
        </div>
        <Forecast
            :value="this.temperature"
            :high="this.temperatureMax"
            :low="this.temperatureMin"
            :icon="this.weatherIcon"
            :descriptionText="this.descriptionText"
        ></Forecast>

        <Weather
            :location="this.location"
            :descriptionText="this.descriptionText"
        ></Weather>
        <Stats
            :humidity="this.humidity"
            :windSpeed="this.windSpeed"
            :cloudiness="this.cloudiness"
        ></Stats>
        </div>
    </div>

</template>

<script>
import Weather from './Weather'
import Forecast from './Forecast'
import Stats from './Stats'

export default {
    name: 'SecureWeather',

    components: {
        Weather,
        Forecast,
        Stats
    },

    data() {
        return {
            pop: 0,
            windSpeed: 0,
            temperature: 0,
            humidity: 0,
            cloudiness: 0,
            temperatureMax: 0,
            temperatureMin: 0,
            locationPermission: false,
            location: '',
            descriptionText: 'Securing and fetching location',
            weatherIcon: require('../assets/icons/weather/cloud.svg'),
            predictionData: null,
            appKey: 'a3e7bdc246b811691b06aab13ccb0dbb'
        }
    },
    mounted: function () {
        this.$nextTick(function () {
            if (navigator.onLine) {
                var app = this;
                pointng.getLocation().then(function(prediction) {
                    if (prediction.city) {
                        app.locationPermission = true
                    }
                    app.updatePrediction(prediction)
                })

            }
        })
    },
    methods: {

        updatePrediction: async function(prediction) {

            try {
                this.predictionData = await this.fetchForecast(prediction);
            } catch (e) {
                this.predictionData = this.getErrorData();
            }
            this.updateData(this.predictionData, prediction);
        },
        fetchForecast: async function (prediction) {
            let appId = this.appKey;

            if (!this.locationPermission) {
                let endpoint = `https://api.openweathermap.org/data/2.5/weather?q=${prediction.capital}&appid=${appId}&units=metric`;
                let response = await fetch(endpoint);
                return await response.json();
            } else {
                let endpoint = `https://api.openweathermap.org/data/2.5/weather?q=${prediction.city}&appid=${appId}&units=metric`;
                let response = await fetch(endpoint);
                return await response.json();
            }    

        },
        getErrorData: function() {
            return {
                clouds: { all: 0 },
                wind: { speed: 0 },
                main: {
                    humidity: 0,
                    temp: 0,
                    temp_max: 0,
                    temp_min: 0,
                },
                weather: [
                    {
                        id: 0,
                        descriptionText: 'An error occured.'
                    }
                ],
                name: null,
                sys: {
                    country: null
                }
            };
        },
        updateData: function (data, prediction) {
            this.cloudiness = data.clouds.all;
            this.windSpeed = data.wind.speed;
            this.humidity = data.main.humidity;
            this.temperature = Math.round(data.main.temp);
            this.temperatureMax = Math.round(data.main.temp_max);
            this.temperatureMin = Math.round(data.main.temp_min);
            if (!this.locationPermission) {
                this.location = this.formatLocation(prediction.capital, null, prediction.country);
            } else {
                this.location = this.formatLocation(data.name, prediction.state, prediction.country);
            }      
            this.descriptionText = data.weather[0].description;
            this.weatherIcon = "https://openweathermap.org/img/w/" + data.weather[0].icon + ".png";
        },
        formatLocation: function (city, state, country) {

            if (!this.locationPermission) {

                if (city === null && country === null) {
                    return '';
                }
        
                return `This service requires your location permission.`;

            } else {

                if (city === null && country === null && state === null) {
                    return '';
                }
        
                return `Near ${city}, ${state}, ${country}`;

            }

        }

    }
}
</script>

<style scoped>
.main-container {
    width: 100%;
    height: 100%;
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    box-shadow: 0 19px 38px rgba(0,0,0,0.30), 0 15px 12px rgba(0,0,0,0.22);
    background: linear-gradient(to bottom right, #bfc0e4, #8b98e4) no-repeat;
}
.circle-container {
    display: flex;
    justify-content: center;
    align-items: center;
}

.phone {
    box-sizing: border-box;
    width: 100%;
    height: 100%;
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
    padding-bottom: 65px;
    padding-left: 25px;
    padding-right: 25px;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    border-radius: 30px;
    overflow: none;
    box-shadow: 0px 0px 0px 10px rgba(0, 0, 0, 0.08);
}

.circle {
    width: 25px;
    height: 25px;
    background-color: #2c2b361a;
    border-radius: 50px;
    align-items: 'center';
}

.inner-circle {
    width: 15px;
    height: 15px;
    margin-left: 5px;
    margin-top: 5px;
    background-color: #2c2b361a;
    border-radius: 50px;
}


@media screen and (min-width: 450px) {
    .main-container {
        width: 325px;
        height: 620px;
        border-radius: 25px;
    }
}

@media only screen and (max-width: 450px) {
  /* For mobile phones: */
    .phone {
        border-radius: 0px;
    }
    
    .circle {
        opacity: 0;
        display: none;
    }

    .inner-circle {
        opacity: 0;
        display: none;
    }

}
</style>
