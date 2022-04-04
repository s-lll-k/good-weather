<template>
    <form class="search">
        <input class="search__input" v-model="cityName" type="text" placeholder="Укажите город">
        <button class="search__btn" @click.prevent="indicateCity">
            <img src="/icons/magnify.svg" alt="искать">
        </button>
    </form>
</template>

<script>
/* eslint-disable */
    export default {
        data(){
            return {
                cityName: ''
            }
        },
        methods: {
            indicateCity(){
                this.$emit('indicateCity', this.cityName)
            }
        }
    }
</script>

<style lang="scss" scoped>
    .search{
        height: 85px;
        display: flex;
        align-items: center;
        &__input{
            width: 100%;
            background-color: transparent;
            border: none;
            padding: 0;
            height: 35px;
            box-shadow: -1px 1px 0px 2px rgba(99, 70, 40, 0.576);
            padding: 0 30px;
            outline: none;
        }
        &__btn{
            display: flex;
            align-items: center;
            justify-content: center;
            width: 35px;
            height: 35px;
            padding: 0;
            background-color: transparent;
            border: none;
            box-shadow: -1px 1px 0px 2px rgba(99, 70, 40, 0.576);
            cursor: pointer;
            margin-left: 10px;
            & > img{
                width: 20px;
                height: 20px;
                object-fit: contain;
                object-position: center;
            }
        }
    }
</style>