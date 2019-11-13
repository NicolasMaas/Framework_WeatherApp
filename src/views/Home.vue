<template>
    <div class="o-container">
        <!-- Image -->
        <img class="c-weather__img" src="@/assets/images/cloud.png" />
        <div class="o-row">
            <div class="c-weather">
                <div class="c-weather--info">
                    <!-- Temperature -->
                    <p class="c-weather__temp">{{ Math.round(locationData.main.temp) }}°</p>

                    <!-- Location -->
                    <h1 class="c-weather__title">
                        {{ locationData.name }}
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="c-weather__title--icon"
                            viewBox="0 0 25.456 25.456"
                        >
                            <path
                                d="M7.5,0,15,21,7.5,13.5,0,21Z"
                                transform="translate(14.849) rotate(45)"
                                fill="#fff"
                            />
                        </svg>
                    </h1>

                    <!-- Time -->
                    <p class="c-weather__time">Now</p>

                    <!-- Icon -->
                    <button v-on:click="changeBackground(rainColor)" class="c-weather--button">
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="c-weather__icon"
                            width="27"
                            height="16"
                            viewBox="0 0 27 16"
                        >
                            <g id="Menu" transform="translate(-49 -737)">
                                <rect
                                    id="Rectangle_4"
                                    data-name="Rectangle 4"
                                    width="27"
                                    height="2"
                                    rx="1"
                                    transform="translate(49 737)"
                                    fill="#fff"
                                />
                                <rect
                                    id="Rectangle_5"
                                    data-name="Rectangle 5"
                                    width="27"
                                    height="2"
                                    rx="1"
                                    transform="translate(49 744)"
                                    fill="#fff"
                                />
                                <rect
                                    id="Rectangle_6"
                                    data-name="Rectangle 6"
                                    width="19"
                                    height="2"
                                    rx="1"
                                    transform="translate(49 751)"
                                    fill="#fff"
                                />
                            </g>
                        </svg>
                    </button>

                    <!-- Submenu -->
                    <section class="is-visible"></section>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "home",
    data() {
        return {
            rainColor: "#005ca3",
            sunnyColor: "#0fcbff",
            cloudColor: "#04a6db",

            location: null,
            gettingLocation: false,
            errorStr: null,
            gotLocation: false,
            locationData: ""
        };
    },

    created() {
        //do we support geolocation
        if (!("geolocation" in navigator)) {
            this.errorStr = "Geolocation is not available.";
            return;
        }

        this.gettingLocation = true;

        // get position
        navigator.geolocation.getCurrentPosition(
            pos => {
                this.gettingLocation = false;
                this.location = pos;
                this.gotLocation = true;

                if (this.gotLocation === true) {
                    this.getData();
                }

                console.log(this.location);
            },
            err => {
                this.gettingLocation = false;
                this.errorStr = err.message;
            }
        );
    },

    methods: {
        async getData() {
            console.log("Lat: ", this.location.coords.latitude);
            console.log("Lon: ", this.location.coords.longitude);

            const lon = this.location.coords.longitude;
            const lat = this.location.coords.latitude;

            const response = await fetch(
                `http://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=e223a51a057a8a5cf039768938969d78&units=metric`
            );

            const json = await response.json();
            this.locationData = json;

            if (this.locationData.weather.main == "Clouds") {
                changeBackground(this.cloudColor);
            } else if (this.locationData.weather.main == "Sunny") {
                changeBackground(this.sunnyColor);
            } else if (this.locationData.weather.main == "Rain") {
                changeBackground(this.rainColor);
            }

            console.log(JSON.stringify(json, null, 4));
        },

        changeBackground(color) {
            document.documentElement.style.setProperty("--global-bg", color);
        }
    }
};
</script>

<style lang="scss" scoped>
@import "@/assets/style/1-settings/colors.scss";
@import "@/assets/style/6-components/weather.scss";

.is-visible {
    min-height: 100%;
}
</style>
