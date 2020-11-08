<template>
    <section>
        <div class="cloudiness">
            <img src="../assets/icons/cloud-2.svg" alt="cloudiness">{{ cloudiness }}&nbsp;&percnt;
        </div>
        <div class="wind-speed">
            <img src="../assets/icons/wind.svg" alt="wind speed">{{ windSpeed }}&nbsp;m/s
        </div>
        <div class="humidity">
            <img src="../assets/icons/humidity.svg" alt="humidity">{{ humidity }}&nbsp;&percnt;
        </div>
    </section>
</template>

<script>
export default {
    name: 'Stats',

    props: {
        cloudiness: {
            type: Number,
            required: true
        },
        windSpeed: {
            type: Number,
            required: true
        },
        humidity: {
            type: Number,
            required: true
        }
    }
}
</script>

<style scoped>
section {
    width: 100%;
    flex-direction: row;
    justify-content: space-evenly;
}
.cloudiness {
    margin-bottom: 15px;
}
.cloudiness img {
    width: 38px;
    height: 38px;
    margin-right: 30px;
     margin-left: 5px;
    vertical-align: middle;
}
.wind-speed {
    margin-bottom: 15px;
}
.wind-speed img {
    width: 38px;
    height: 38px;
    margin-right: 30px;
    margin-left: 5px;
    vertical-align: middle;
}
.humidity img {
    width: 38px;
    height: 38px;
    margin-right: 30px;
     margin-left: 5px;
    vertical-align: middle;
}
</style>
