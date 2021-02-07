<template>
      <ion-card>
        <ion-card-header>
          <ion-card-subtitle>{{city.code}}</ion-card-subtitle>
          <ion-card-title>{{city.nom}}</ion-card-title>
        </ion-card-header>
        <ion-card-content>
          <ion-item class="section">
            <div class="info">Département<p>{{city.codeDepartement}}</p></div>
          </ion-item>
          <ion-item class="section">
            <div class="info">Région<p>{{city.codeRegion}}</p></div>
          </ion-item>
          <ion-item class="section">
            <div class="info">Codes postaux<p>{{postaux}}</p></div>
          </ion-item>
          <ion-item class="section">
            <div class="info">Population<p>{{city.population}}</p></div>
          </ion-item>
        </ion-card-content>
      </ion-card>
</template>

<script>
import { IonCard, IonCardHeader, IonCardSubtitle, IonCardTitle, IonCardContent, IonItem} from '@ionic/vue';

export default  {
  name: 'CommunesResult',
  components: { IonCard, IonCardHeader, IonCardSubtitle, IonCardTitle, IonCardContent, IonItem  },
  props: ['city'],
  data() {
    return {
      postaux: ""
    }
  },
  mounted() {
    this.getPostaux()
  },
  methods: {
    getPostaux(){
      this.postaux = this.city.codesPostaux.join(', ')
    }
  },
}
</script>
<style>
.section{
  width: 100%;
}
.info{
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  color: blue;
}
.info p{
  color: red;
  text-align: right;
}
</style>