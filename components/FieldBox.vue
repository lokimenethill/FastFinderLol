<template>
  <v-row justify="center" align="center">
    <v-col>
      <v-card class="">
        <v-select
          v-model="regionSelected"
          :items="region"
          label="Region"
          outlined
          dense
        ></v-select>
        <v-textarea
          outline
          v-model="inputText"
          label="Inserta el texto del chat de League of Legends"
        ></v-textarea>
        Datos en una linea:
        <p v-show="!isActive">{{ outputText }}</p>

        <v-btn @click="find()" color="info" :disabled="isActive">Buscar</v-btn>
        <span v-show="isActive">Faltan datos de busqueda</span>
      </v-card>
    </v-col>
  </v-row>
</template>
<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      inputText: '',
      regionSelected: '',
      region: ['lan', 'las', 'na'],
      lang: 0,
      isActive: true,
    }
  },
  computed: {
    outputText() {
      let replacedText = ''
      if (this.regionSelected == 'lan' || this.regionSelected == 'las') {
        replacedText = this.inputText.replace(/se unió a la sala/g, ',')
      } else {
        replacedText = this.inputText.replace(/joined the lobby/g, ',')
      }
      let cleanedText = replacedText.replace(/(\r\n|\n|\r)/gm, '')
      let summonerArray = cleanedText.split(',')
      let summonerNames = []
      let summonerNamesOneLiner = ''
      for (let i = 0; i < summonerArray.length; i++) {
        if (summonerArray[i] != '') {
          summonerNames.push(summonerArray[i])
          summonerNamesOneLiner += summonerArray[i] + ','
        }
      }
      //console.log(summonerNames);
      return summonerNamesOneLiner
    },
  },
  methods: {
    find() {
      let replacedText = ''
      if (this.regionSelected == 'lan' || this.regionSelected == 'las') {
        replacedText = this.inputText.replace(/se unió a la sala/g, ',')
      } else {
        replacedText = this.inputText.replace(/joined the lobby/g, ',')
      }
      let cleanedText = replacedText.replace(/(\r\n|\n|\r)/gm, '')
      let summonerArray = cleanedText.split(',')
      let summonerNames = []
      let summonerNamesOneLiner = ''
      for (let i = 0; i < summonerArray.length; i++) {
        if (summonerArray[i] != '') {
          summonerNames.push(summonerArray[i])
          summonerNamesOneLiner += summonerArray[i] + ','
        }
      }
      console.log(summonerNames)
      let tempUrl = ''
      for (let x = 0; x < summonerNames.length; x++) {
        tempUrl = `https://www.leagueofgraphs.com/summoner/${this.regionSelected}/${summonerNames[x]}`
        console.log(tempUrl)
        window.open(tempUrl, '_blank')
      }
      tempUrl = `https://lan.op.gg/multisearch/${this.regionSelected}?summoners=${summonerNamesOneLiner}`
      console.log(tempUrl)
      window.open(tempUrl, '_blank')
    },
  },
  watch: {
    regionSelected() {
      if (this.regionSelected != '' && this.inputText != '') {
        this.isActive = false
      } else {
        this.isActive = true
      }
    },
    inputText() {
      if (this.regionSelected != '' && this.inputText != '') {
        this.isActive = false
      } else {
        this.isActive = true
      }
    },
  },
}
</script>
