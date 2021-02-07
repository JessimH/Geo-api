<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Accueil</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content fullscreen class="ion-padding" scroll-y="false">
      <div class="accueil">
        <img src="https://blog.francetvinfo.fr/deja-vu/files/2016/08/marianne-600x353.png" alt="">
        <h1>Bienvenue</h1>
        <p>Sur cette application vous pourrez retrouver toutes les informations essentielles concernant les communes, départements ou régions française.</p>
        <p>Toutes ses informations nous sont fournis par
          <a target="_blank" href="https://geo.api.gouv.fr/decoupage-administratif">l'API officiel du gouvernement français</a>
        </p>
        <p>Bonne recherches a tous!!</p>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';

export default  {
  name: 'Accueil',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage }
}
</script>
<style lang="css">
.accueil{
  font-size: 1.1em;
}

.accueil h1{
  font-weight: 600;
}

.accueil a{
  text-decoration: none;
  font-weight: 500;
}
  
</style>