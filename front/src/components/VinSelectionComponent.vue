<template>
  <q-item class="text-center" id="vin_jour" v-for="vinsOne in listVinsOne" :key="vinsOne.idBoisson">
    <div class="q-mt-sm vin_jour_img">
      <img role="button" data-fancybox="" :src="
        'https://nosvinsdumonde.com/assets/img/' +
        vinsOne.typeBoisson +
        '/' +
        vinsOne.imageBoisson +
        ''
      " class="img-fluid rounded-start" alt="" />
    </div>

    <div class="vin_jour_title">
      <h3 class="text-white no-border" style="padding: 0 0; margin-bottom: 0">
        <q-item class="text-white fw-bold text-decoration-none"
          :to="'/' + vinsOne.typeBoisson + '/' + vinsOne.idBoisson">{{ decode(vinsOne.nomBoisson) }}
          {{ vinsOne.millesimeBoisson }}</q-item>
      </h3>
    </div>

    <div class="q-mt-lg">
      <span class="badge_region">{{ vinsOne.regionBoisson }}</span>
    </div>
    <div class="q-mt-md appellation">
      <span class="text-white">{{ vinsOne.apellationBoisson }}</span>
    </div>
    <div class="q-mt-sm prix text-white">
      <span class="chiffre"><span :class="vinsOne.planBoisson == 1 ? 'text-warning' : ''"
          :style="vinsOne.planBoisson == 1 ? 'text-decoration: line-through!important; font-size: 18px;' : 'font-size: 30px;'">{{
              replaceVirgule(vinsOne.prixBoisson)
          }} €</span> <span v-if="vinsOne.planBoisson == 1">{{
    replaceVirgule(vinsOne.remiseBoisson)
}} €</span></span>
    </div>
    <div class="q-mb-lg contenance">
      <span class="text-white">{{ $t('CONTENANCE') }} {{ vinsOne.contenanceBoisson }}</span>
    </div>

    <q-btn :to="'/' + vinsOne.typeBoisson + '/' + vinsOne.idBoisson" push color="warning">
      <q-item-section avatar style="min-width: 20px; padding-right: 0; text-transform: uppercase;">
        <q-icon size="15px" name="fa-solid fa-chevron-right" />
      </q-item-section>
      {{ $t('DECOUVRIR_BTN') }}
    </q-btn>
  </q-item>
</template>

<script>
let decoder;

export default {
  name: 'vinsNameOne',
  methods: {
    // Source: https://github.com/vuejs/vue/blob/v2.6.14/src/compiler/parser/entity-decoder.js
    decode(html) {
      decoder = decoder || document.createElement('div');
      decoder.innerHTML = html;
      return decoder.textContent;
    },
    replaceVirgule(html) {
      return (html + '').replace('.', ',');
    },
  },
  components: {},
  props: {
    listVinsOne: Array,
  },
};
</script>
