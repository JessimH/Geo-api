<template>
  <ion-page>
    <ion-tabs>
      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="accueil" href="/tabs/accueil">
          <ion-icon :icon="homeOutline" />
          <ion-label>Accueil</ion-label>
        </ion-tab-button>
          
        <ion-tab-button tab="communes" href="/tabs/communes">
          <ion-icon :icon="pinOutline" />
          <ion-label>Communes</ion-label>
        </ion-tab-button>
        
        <ion-tab-button tab="departements" href="/tabs/departements">
          <ion-icon :icon="navigateCircleOutline" />
          <ion-label>Departements</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="regions" href="/tabs/regions">
          <ion-icon :icon="mapOutline" />
          <ion-label>Régions</ion-label>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script>
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage } from '@ionic/vue';
import { homeOutline, pinOutline, navigateCircleOutline, mapOutline } from 'ionicons/icons';

export default {
  name: 'Tabs',
  components: { IonLabel, IonTabs, IonTabBar, IonTabButton, IonIcon, IonPage },
  setup() {
    return {
      homeOutline, 
      pinOutline, 
      navigateCircleOutline,
      mapOutline
    }
  }
}
</script>