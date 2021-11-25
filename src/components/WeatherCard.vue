<template>
    <ion-page>
        <ion-card>
            <img :src="cityimgprop" class="fit" /> 
            <ion-grid>
                <ion-row>
                    <ion-col>
                        <ion-card-header >
                            <ion-card-title>{{wordprop.name}}, {{wordprop.main.temp}}°C</ion-card-title>
                            <ion-card-subtitle class="head"> <ion-icon :icon="findIcon(wordprop.weather[0].main)" size="large"></ion-icon> {{wordprop.weather[0].main}}</ion-card-subtitle>
                        </ion-card-header>
                    </ion-col>
                    <ion-col>
                        <ion-card-header>
                            <ion-card-subtitle>Minimal and maximal temp in the day</ion-card-subtitle>
                            <ion-card-title>{{wordprop.main.temp_min+'°-'+wordprop.main.temp_max}}°</ion-card-title>
                        </ion-card-header>
                    </ion-col>
                </ion-row>
                
            </ion-grid>
                

            <ion-card-content>
                <ion-grid>
                    <ion-row>
                        <ion-col>
                            <ion-card-subtitle><ion-icon :icon="water"></ion-icon> Humidity</ion-card-subtitle>
                            <ion-card-title>{{wordprop.main.humidity}}%</ion-card-title>
                        </ion-col>
                        <ion-col>
                            <ion-card-subtitle><img class="wind" src='../assets/pressure.svg' alt="pressure"> Pressure</ion-card-subtitle>
                            <ion-card-title>{{wordprop.main.pressure}} hPa</ion-card-title>
                        </ion-col>
                    </ion-row>
                    <ion-row>
                        <ion-col>
                            <ion-card-subtitle><img class="wind" src='../assets/wind.svg' alt="wind">  Wind</ion-card-subtitle>
                            <ion-card-title>{{wordprop.wind.speed}} m/s</ion-card-title>
                        </ion-col>
                        <ion-col>
                            <ion-card-subtitle><ion-icon :icon="cloudyOutline"></ion-icon> Cloudiness</ion-card-subtitle>
                            <ion-card-title>{{wordprop.clouds.all}}%</ion-card-title>
                        </ion-col>
                    </ion-row>
                </ion-grid>
            </ion-card-content>
        </ion-card>
        
    </ion-page>
</template>
<script>
//import and register components
import { IonCard, IonCardContent, IonIcon} from '@ionic/vue';
// import all components from 'ionicons/icons'
import { sunny, cloudy, rainy, snow, water, cloudyOutline } from 'ionicons/icons';
export default{
    name: 'WeatherCard',
    components: { IonCard, IonCardContent, IonIcon},
    setup:()=>{
        return{
            sunny,
            cloudy,
            rainy,
            snow,
            water,
            cloudyOutline
        }
    },
    data() {
        return {
            icon: '',
        }
    },
    props: {
        wordprop: String,
        cityimgprop: String
    },
    methods:{
        findIcon(word){
            if(word.toLowerCase()=='sunny' || word.toLowerCase()=='clear') return this.sunny;
            else if (word.toLowerCase()=='rain') return this.rainy;
            else if (word.toLowerCase()=='snow') return this.snow;
            else if (word.toLowerCase()=='clouds') return this.cloudy;
        }   
    }
}
</script>
<style>
.fit{
    width: 100%;
    height: auto;
    max-height: 200px;
    object-fit: cover;
/*    it shows center of image */
    object-position: center;
}
.head{
    display: flex;
}
.wind{
    width: 16px;
}
</style>