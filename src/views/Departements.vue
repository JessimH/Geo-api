<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Departements</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Departements</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-toolbar class="search">
        <ion-item>
          <ion-label>Départements</ion-label>
          <ion-select v-model="search">
            <ion-select-option 
              v-for="departement in departements"
              :key="departement"
              :value="departement.code">
                {{departement.code}} - {{departement.nom}}
              </ion-select-option>
          </ion-select>
        </ion-item>
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
        v-if="succes > 0"
        class="succes">{{succes}} résultats</div>
      <div>
        <div v-if="loading">
          <Loading/>
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
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonLabel, IonSelect, IonSelectOption, IonButton, IonItem } from '@ionic/vue';
import CommunesResult from '../components/CommunesResult.vue'
import Loading from '../components/Loading.vue'


export default  {
  name: 'Departements',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, CommunesResult, IonLabel, IonSelect, IonSelectOption, IonButton, IonItem, Loading},
  data() {
    return {
      departements: [],
      search: "",
      citys: [],
      error: "",
      succes: "",
      loading: false
    }
  },
  mounted() {
    this.fetchDepartement()
  },
  methods: {
    fetchDepartement(){
      fetch(`https://geo.api.gouv.fr/departements`)
      .then(res => res.json())
      .then(data => {
          this.departements = data
      })
    },
    fetchCommune(){
      this.loading = true

      fetch(`https://geo.api.gouv.fr/departements/${this.search}/communes`)
      .then(res => res.json())
      .then(data => {
          console.log(data.length)
          this.citys = data
          this.succes = this.citys.length
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