<template>
      <ion-card>
        <ion-card-header>
          <ion-card-title>{{departement.nom}}</ion-card-title>
          <ion-card-subtitle>Code INSEE: {{departement.code}}</ion-card-subtitle>
        </ion-card-header>
      </ion-card>
</template>

<script>
import { IonCard, IonCardHeader, IonCardSubtitle, IonCardTitle} from '@ionic/vue';

export default  {
  name: 'DepartementsResult',
  components: { IonCard, IonCardHeader, IonCardSubtitle, IonCardTitle},
  props: ['departement'],
  data() {
    return {
    }
  },
  mounted() {
  },
  methods: {
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