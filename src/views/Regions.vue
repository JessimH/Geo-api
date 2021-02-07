<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Regions</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Regions</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-toolbar class="search">
        <ion-item>
          <ion-label>Regions</ion-label>
          <ion-select v-model="search">
            <ion-select-option 
              v-for="region in regions"
              :key="region"
              :value="region.code">
                {{region.code}} - {{region.nom}}
              </ion-select-option>
          </ion-select>
        </ion-item>
        <ion-button 
          :disabled="!search" 
          @click="fetchDepartements" 
          expand="block">Rechercher</ion-button>
        <ion-button 
          v-if="search"
          color="light" 
          @click="reset" 
          expand="block">Réinitialiser</ion-button>
      </ion-toolbar>
      <div 
        v-if="succes > 0"
        class="succes">{{succes}}</div>
      <div>
        <div v-if="loading">
          <Loading />
        </div>
        <DepartementsResult
          v-for="departement in departements"
          :key="departement.code"
          :departement="departement"
        />
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonLabel, IonSelect, IonSelectOption, IonButton, IonItem } from '@ionic/vue';
import DepartementsResult from '../components/DepartementsResult.vue'
import Loading from '../components/Loading.vue'


export default  {
  name: 'Departements',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, DepartementsResult, IonLabel, IonSelect, IonSelectOption, IonButton, IonItem, Loading },
  data() {
    return {
      regions: [],
      search: "",
      departements: [],
      error: "",
      succes: "",
      loading: false
    }
  },
  mounted() {
    this.fetchRegions()
  },
  methods: {
    fetchRegions(){
      fetch(`https://geo.api.gouv.fr/regions`)
      .then(res => res.json())
      .then(data => {
          this.regions = data
      })
    },
    fetchDepartements(){
      this.loading = true
      fetch(`https://geo.api.gouv.fr/regions/${this.search}/departements`)
      .then(res => res.json())
      .then(data => {
          console.log(data)
          this.departements = data
          this.citys.length > 1 ? this.succes = `${this.citys.length} résultats` : this.succes = `${this.citys.length} résultat`
          this.loading = false
      })
    },
    reset(){
      this.departements = [],
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