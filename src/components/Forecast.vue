<template>
    <div>
        <section>
            <img class="icon" :src="icon" :alt="descriptionText">
            <div class="temp-value">{{ (symbol === 'C')? value : fValue }}</div>
            <div class="temp-right">
                <div class="temp-symbol">
                    <a href="#" @click.prevent="toggleTemp">&deg;{{ symbol }}</a>
                </div>

            </div>

        </section>
        <section style="margin-left: 65px; margin-top: -25px;">
            <span>{{ (symbol === 'C')? low : fMin }}</span>&deg; /&nbsp;
            <span>{{ (symbol === 'C')? high : fMax }}</span>&deg;
        </section>
    </div>
</template>

<script>
export default {
    name: 'Forecast',

    props: {
        value: {
            type: Number,
            required: true
        },
        high: {
            type: Number,
            required: true
        },
        low: {
            type: Number,
            required: true
        },
        icon: {
            type: String,
            required: true
        },
        descriptionText: {
            type: String,
            required: true
        }
    },

    data: function() {
        return {
            scale: 'Celcius'
        }
    },

    computed: {
        symbol() {
            return this.scale.charAt(0);
        },

        fValue() {
            return this.fahrenheit(this.value);
        },

        fMax() {
            return this.fahrenheit(this.high);
        },

        fMin() {
            return this.fahrenheit(this.low);
        }
    },

    methods: {
        fahrenheit(value) {
            return Math.floor((value * 1.8) + 32);
        },

        toggleTemp() {
            (this.scale === 'Celcius')? this.scale = 'Fahrenheit' : this.scale = 'Celcius';
        }
    }
}
</script>

<style scoped>
section {
    display: flex;
    flex-direction: row;
}

.temp-value {
    font-size: 6em;
    color: rgba(255, 255, 255, 0.85);
}

.temp-right {
    margin-top: 25px;
}

.temp-symbol {
    padding-top: 5px;
    font-size: 1.5em;
    font-weight: bold;
    color: rgba(255, 255, 255, 0.85);
}

.icon {
    width: 50px;
    height: 50px;
    margin-top: 45px;
    margin-right: 5px;
}

</style>
