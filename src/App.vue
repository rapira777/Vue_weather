<!-- https://www.youtube.com/watch?v=TiBCLraUFvA -->
<!-- 27c6e0fb796b0caa8fb014468ed24bfb -->
<script>
import axios from 'axios'
export default {
    data() {
        return {
            city: "",
            error: "",
            info: null,
        }
    },
    computed:{
        cityName() {
            return "< " + this.city + " >"
        },
        showTemp(){
            return "Температура: " + this.info.main.temp
        },
        showFeelsLike() {
            return "Ощущается как: " + this.info.main.feels_like
        },
        showMinTemp(){
            return "Температура Min: " + this.info.main.temp_min
        },
        showMaxTemp(){
            return "Температура Max: " + this.info.main.temp_max
        },
        
    },
    methods: {
         getWeather() {
            if(this.city.trim().length<2){
                this.error = "Нужно название более одного символа."
                return false
            }
            this.error=''

            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=27c6e0fb796b0caa8fb014468ed24bfb`)
            .then(res=>(this.info=res.data))
        
        }
        }
}
</script>

<template>
    <div class="wrapper"> 
        <h1>Погодное приложение</h1>
        <p>Узнать погоду в {{city=="" ? "вашем городе" : cityName}}</p>
        <!-- <input type="text" v-on:input="this.city=$event.target.value" placeholder="Введите город"> -->
        <!-- <input type="text" @input="this.city=$event.target.value" placeholder="Введите город"> -->
        <input type="text" v-model="city" placeholder="Введите город,напр.Moscow">
    
        <!-- <button v-show="city !='' ">Узнать погоду</button> -->
        <button v-if="city !='' " @click="getWeather()">Узнать погоду</button>
        <button disabled v-else>Введите название города</button>
        <p class="error">{{error}}</p>
        <!-- <p v-show="info != null">{{info.main.temp}}</p> -->
        <div v-if="info != null">
            <p>{{showTemp}}</p>
            <p>{{showFeelsLike}}</p>
            <p>{{showMinTemp}}</p>
            <p>{{showMaxTemp}}</p>
        </div>
        
    </div>
</template>

<style scoped>
.error {
    color: #d03939;
}
.wrapper {
    width: 900px;
    height: 500px;
    border-radius: 50px;
    padding: 20px;
    background: #1f0f24;
    text-align: center;
    color: #fff;
}
.wrapper h1 {
    margin-top: 50px;
}
.wrapper p {
    margin-top: 20px;
}

.wrapper input {
    margin-top: 30px;
    background: transparent;
    border: 0;
    border-bottom: 2 px solid #110813;
    color: #fcfcfc;
    font-size: 14px;
    padding: 5px 8px;
    outline: none;
}

.wrapper input:focus {
    border-bottom-color: #6e2d7d;
}

.wrapper button {
    background: #e3bc4b;
    color: #fff;
    border-radius: 10px;
    border: 2px solid #b99935;
    padding: 10px 15px;
    margin-left: 20px;
    cursor: pointer;
    transition: transorm 500ms ease;
}
.wrapper button:hover {
    transform: scale(1.1) translateY(-5px);
}

.wrapper button:disabled {
    background: #746027;
    cursor: not-allowed;
}
</style>