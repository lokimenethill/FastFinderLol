<template>
  <v-row justify="center" align="center">
    <v-col >
      <title-top></title-top>
      <field-box></field-box>
      <footer-cards-ad></footer-cards-ad>
    </v-col>
  </v-row>
</template>

<script>
import FieldBox from '../components/FieldBox.vue'
import titleTop from '../components/titleTop.vue'
import footerCardsAd from '../components/footerCardsAd.vue'
export default {
  components:{FieldBox,titleTop,footerCardsAd},
  name: 'IndexPage',
}
</script>
