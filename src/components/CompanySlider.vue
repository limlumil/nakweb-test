<template>
  <div>
    <h2>Exercice - Reproduire le composant :</h2>
    <BaseSlider v-if="dataItems.length" class="company-slide" :totalSlides="dataItems.length" :autoPlay="true"
      :slideDuration="5000">
      <template v-slot="slider">
        <card-slider
        :image="require(`@/assets${dataItems[slider.currentIndex].image}.jpg`)"
        :alt="dataItems[slider.currentIndex].title"
        :title="dataItems[slider.currentIndex].title "
        :description ="dataItems[slider.currentIndex].text"
        :buttontext="dataItems[slider.currentIndex].cta"
        :color="`#000`"
        :backgroundcolor="`#bfef06`"
        :link= '`${dataItems[slider.currentIndex].to}`'
        @buttonClick= "(e)=>handleCta(e)"
        />
      </template>
    </BaseSlider>

    <h2>Exercice - Le slider doit être réutilisable :</h2>
    <p>Ici, nous utilisons le même composant "BaseSlider" et nous lui fournissons uniquement des images à faire défiler.
    </p>
    <BaseSlider v-if="dataItems.length" class="company-slide2" :totalSlides="dataItems.length" :autoPlay="true"
      :control="false" :slideDuration="5000">
      <template v-slot="slider">
        <card-slider
        :image="require(`@/assets${dataItems[slider.currentIndex].image}.jpg`)"
        :alt="dataItems[slider.currentIndex].title"
        />
        
      </template>
    </BaseSlider>
  </div>
</template>

<script>
import CardSlider from './slider/CardSlider.vue';
import BaseSlider from './slider/BaseSlider.vue'

export default {
  name: 'CompanySlider',
  components: {
    BaseSlider,
    CardSlider,
  },
  data() {
    return {
      dataItems: [
        {
          title: 'Une entreprise familiale',
          image: '/images/company/team',
          cta: 'Qui sommes-nous ?',
          to: '/nous/',
          text: `Spécialisés dans la gravure, la signalétique et l’impression depuis plus de 60 ans à Grenoble nous proposons également nos services en ligne.`,
        },
        {
          title: 'Service client à votre écoute',
          image: '/images/company/customer-care',
          cta: 'besoin d’assistance ?',
          text: `Notre équipe au service satisfaction clientèle est prête à vous répondre par email ou téléphone du lundi au vendredi, de 9h à 12h et de 14h à 17h.`,
        },
        {
          title: 'La signalétique déjà disponible !',
          image: '/images/company/signaletique',
          cta: 'Découvrir',
          to: '/signaletique/',
          text: `Vous pouvez maintenant créer des plaques de signalétique en tout genre (pour les pros et les particuliers) avec l’éditeur que vous connaissez.`,
        },
        {
          title: 'Paiement sécurisé',
          image: '/images/company/payment',
          cta: 'En savoir plus',
          to: '/aide/',
          text: `À chaque étape de la transaction, vos informations bancaires sont cryptées et uniquement réceptionnées par le prestataire choisi.`,
        },
        {
          title: 'Projet important ou original ?',
          image: '/images/company/quotation',
          cta: 'demander un devis',
          text: `Vous avez besoin d’une grande quantité ou une demande spéciale que vous ne pouvez pas satisfaire avec notre éditeur ? Parlons-en.`,
        },
      ],
    }
  },
  methods: {
    handleCta(e) {
      console.log("click on : " + e);
    }
  }
}
</script>

<style lang="scss" scoped>
h2,
p {
  text-align: left;
}

.base-slider {
  &.company-slide {
    width:100%;
    max-width: 400px;
    text-align: left;
    height: fit-content;
    min-height: 450px;

  }

  &.company-slide2 {
    width:100%;
    max-width: 400px;
    min-height: 224px;
  }

}</style>
