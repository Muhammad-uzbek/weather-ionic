<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-searchbar @ionInput="searchword = $event.target.value"  show-cancel-button="focus" search-icon></ion-searchbar>
        <ion-button color="tertiary" @click="putToVal(this.searchword)" slot="end">Search</ion-button>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
        <WeatherCard v-if="weather!=''" :wordprop="weather" :cityimgprop="cityimg" />
        <ion-text v-else class="info" color="tertiary">
          <h3>
            Please type your city to know about weather
          </h3> 
          </ion-text>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage,
  IonHeader,
  IonToolbar,
  IonButton } from '@ionic/vue';
import WeatherCard from '../components/WeatherCard';
export default  {
  name: 'Tab1',
  data() {
    return {
      searchword: '',
      putIt:'',
      apikey:'092f5fa8f0e4d78a253a69fadea959f8',
      weather: '',
      cityimg:'',
      isNotFounded: false,
      imageLinksofCitiesOfUzbekistan:[
        {
          name:'Tashkent',
          url:'https://storage.kun.uz/source/4/WySAZzWh-v3yYmjgSTtkzZcwy6_obVhY.jpg'
        },
        {
          name:'Andijon',
          url:'https://storage.kun.uz/source/thumbnails/_medium/5/fI15NX9vjy3n1GaTcabMUgmBOUnBZiIE_medium.jpg'
        },
        {
          name:'Bukhara',
          url:'https://upload.wikimedia.org/wikipedia/commons/a/a8/2012_Bukhara_7515821196.jpg'
        },
        {
          name:'Namangan',
          url:'https://www.orexca.com/img/namangan/namangan10-10.jpg'
        },
        {
          name:'Samarkand',
          url:'https://upload.wikimedia.org/wikipedia/commons/5/53/Registan_Samarkand_Timurid_Renaissance.jpg'
        },
        {
          name:'Navoi',
          url:'https://lh3.googleusercontent.com/proxy/hAdml2wVi00Ds2_SsXzfjg_iTb1RNQCzDmsdwoygo_7KE6_itb9l_X8nGKhJhw92UkfYJbaZtNrLZu_covV-ToFlvCxakspRVsYB1kX7Rd-_Zw'
        }
      ]
    }
  },
  methods: {
    putToVal(val){
      this.putIt = val;
      this.fetchWeather(val);
      this.fetchImg(val.toLowerCase());
    },
    fetchWeather(city) {
      fetch(`https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${this.apikey}&lang=pt_b`)
        .then(response => response.json())
        .then(data => {
          this.weather = data;
          
        })
        .catch(error => console.error(error));
    },
    fetchImg(city){
      for(let i=0;i<this.imageLinksofCitiesOfUzbekistan.length;i++){
        if(this.imageLinksofCitiesOfUzbekistan[i].name.toLowerCase()==city){
          this.cityimg = this.imageLinksofCitiesOfUzbekistan[i].url;
          break;
        }
        else{
          this.isNotFounded = true;
        }
      }
      if(this.isNotFounded){
      fetch(`https://api.teleport.org/api/urban_areas/slug:${city}/images/`)
        .then(response => response.json())
        .then(data => {
          this.cityimg = data.photos[0].image.mobile;
        })
        .catch(error => console.error(error));
        }
      }
  },
  components: { IonHeader, IonToolbar, IonPage, IonButton, WeatherCard }
}
</script>
<style>
.info{
  text-align: center;
  padding: 10px;
  width: 100%;
  display: flex;
  justify-content: center;
}
.info h3{
  width: 70%;
}
</style>