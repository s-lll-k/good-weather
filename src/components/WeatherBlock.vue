<template>
    <div class="weather__wrapper">
        <div class="weather__quote" v-show="!weatherInfo.show && !weatherInfo.error">
            <q class="weather__quote-text">
                Вдохновение можно найти даже в прогнозе погоды
            </q>
            <span class="weather__quote-author">
                - Хаяо Миядзаки
            </span>
        </div>
        <div class="weather__error" v-show="weatherInfo.error">
            Город {{weatherInfo.city}} не найден :(
        </div>
        <div class="weather__info" v-show="weatherInfo.show">
            <h1 class="weather__description">{{weatherInfo.weather}}</h1>
            <div class="weather__temp">
                <img src="/icons/thermometer.svg" alt="температура">
                <span>{{weatherInfo.temperature}}</span>
            </div>
            <div class="weather__wind">
                <img src="/icons/wind.svg" alt="ветер">
                <span>{{weatherInfo.wind}} м/с</span>
            </div>
            <div class="weather__icon">
                <img :src="`./icons/${weatherInfo.imgCode}.svg`" alt="иконка погоды">
            </div>
        </div>
    </div>
</template>

<script>
/* eslint-disable */
export default {
    props: {
        weatherInfo: {
            type: Object,
            required: true
        }
    },
    data() {
        return {

        }
    }
}
</script>

<style lang="scss" scoped>
    .weather{
        &__info{
            font-size: 30px;
        }
        &__description{
            font-size: 36px;
            font-weight: 700;
        }
        &__wind,
        &__temp{
            display: flex;
            align-items: center;
            & > img{
                width: 60px;
                height: 60px;
                object-fit: contain;
            }
            & > span{
                margin-left: 10px;
            }
        }
        &__icon{
            width: 200px;
            height: 200px;
        }
        &__wrapper{
            padding: 50px 0;
        }
        &__quote{
            &-text{
                display: block;
                font-size: 25px;
            }
            &-author{
                display: block;
                max-width: max-content;
                margin-left: auto;
                margin-top: 10px;
            }
        }
    }
</style>