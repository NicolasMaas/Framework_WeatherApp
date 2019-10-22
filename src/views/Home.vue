<template>
    <div class="o-container">
        <!-- Image -->
        <img class="c-weather__img" src="@/assets/images/cloud.png" />
        <div class="o-row">
            <div class="c-weather">
                <div class="c-weather--info">
                    <!-- Temperature -->
                    <p class="c-weather__temp">18°</p>

                    <!-- Location -->
                    <h1 class="c-weather__title">
                        Belfast
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
            cloudColor: "#04a6db"
        };
    },

    methods: {
        changeBackground(color) {
            document.documentElement.style.setProperty("--global-bg", color);
        }
    }
};
</script>

<style lang="scss" scoped>
@import "@/assets/style/1-settings/colors.scss";
@import "@/assets/style/6-components/weather.scss";

.background-rain {
    background-color: $rain-color;
}

.background-cloud {
    background-color: $cloud-color;
}

.background-sunny {
    background-color: $sunny-color;
}
</style>
