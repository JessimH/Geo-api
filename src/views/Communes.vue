<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Communes</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Communes</ion-title>
        </ion-toolbar>
      </ion-header>
    
      <ion-toolbar class="search">
        <ion-searchbar 
          v-model="search" 
          placeholder="Nom de ville ou code postal"
          @keypress.enter="fetchCommune"></ion-searchbar>
        <ion-button 
          :disabled="!search" 
          @click="fetchCommune" 
          expand="block">Rechercher</ion-button>
        <ion-button 
          v-if="search"
          color="light" 
          @click="reset" 
          expand="block">Réinitialiser</ion-button>
      </ion-toolbar>
      <div 
        v-if="error"
        class="error">{{error}}</div>
      <div 
        v-if="succes"
        class="succes">{{succes}}</div>
      <div>
        <div v-if="loading">
          <Loading />
        </div>
        <CommunesResult
          v-for="city in citys"
          :key="city.code"
          :city="city"
        />
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonSearchbar, IonButton } from '@ionic/vue';
import CommunesResult from '../components/CommunesResult.vue'
import Loading from '../components/Loading.vue'

export default  {
  name: 'Communes',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonSearchbar, CommunesResult, IonButton, Loading },
  data() {
    return {
      search: "",
      citys: [],
      error: "",
      succes: "",
      loading: false
    }
  },
  mounted() {
    
  },
  methods: {
    fetchCommune(){
      let url
      let urlString = `https://geo.api.gouv.fr/communes?nom=${this.search}`
      let urlNumber = `https://geo.api.gouv.fr/communes?codePostal=${this.search}`

      this.search == Number(this.search) ? url = urlNumber : url = urlString

      this.loading = true

      fetch(url)
      .then(res => res.json())
      .then(data => {
          console.log(data)
          this.citys = data
          this.citys.length > 1 ? this.succes = `${this.citys.length} résultats` : this.succes = `${this.citys.length} résultat`
          console.log(this.succes)
          this.error = ""
          this.loading = false
          if(this.citys.length === 0){
            this.error = "Aucun résultat, entrez un nom de ville ou un code postal valide"
            this.succes = ""
          }
      })
    },
    reset(){
      this.citys = [],
      this.search = ""
      this.error = ""
      this.succes = ""
    }
  },
}
</script>
<style lang="css">
  .search{
    padding: 10px;
  }
  .error{
    width: 100%;
    padding: 20px;
    background-color: rgba(255, 0, 0, 0.123);
    font-weight: 600;
    color: red;
  }
  .succes{
    width: 100%;
    padding: 20px;
    background-color: rgba(0, 255, 64, 0.123);
    font-weight: 600;
    color: green;
  }
</style>