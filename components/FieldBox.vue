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
        <p>{{outputText}}</p>
        
        <v-btn @click="find()" color="info" :disabled="isActive">Buscar</v-btn>
        <span v-show="isActive">Faltan datos de busqueda</span>
       
      </v-card>
    </v-col>
  </v-row>
</template>
<script>
export default {
  name: 'IndexPage'
  ,
data(){
    return{
        inputText:'',
        regionSelected:'',
        region: ['lan', 'las','na'],
        dataTrashStringLang:{
          es:['se','unió','a','la','sala'],
          en:[],
        },
        lang:0,
        isActive:true
    }
},
computed:{
        outputText(){
          let selectorArrayLang=[];
            if(this.regionSelected=="lan" || this.regionSelected=="las"){
              selectorArrayLang=this.dataTrashStringLang['es'];
            }else{
              selectorArrayLang=this.dataTrashStringLang['en'];
            }
            let cleanedText = this.inputText.replace(/(\r\n|\n|\r)/gm, " ");
            let summonerArray=cleanedText.split(" ");
            let summonerNames=[]
            let summonerNamesOneLiner = '';
            //console.log(summonerArray)
            for(let i=0;i<selectorArrayLang.length;i++){
              summonerNames=summonerArray.filter(word => word != selectorArrayLang[i]);
              summonerArray=summonerNames;
            }
            for(let i=0;i<summonerNames.length;i++){
              if(i==summonerNames.length-1){
                summonerNamesOneLiner+=summonerNames[i];
              }else{
                summonerNamesOneLiner+=summonerNames[i]+',';
              }
            }
            return summonerNamesOneLiner;
        },
    },
    methods:{
    find(){
      let selectorArrayLang=[];
            if(this.regionSelected=="lan" || this.regionSelected=="las"){
              selectorArrayLang=this.dataTrashStringLang['es'];
            }else{
              selectorArrayLang=this.dataTrashStringLang['en'];
            }
       let cleanedText = this.inputText.replace(/(\r\n|\n|\r)/gm, " ");
            let summonerArray=cleanedText.split(" ");
            let summonerNames=[]
            let summonerNamesOneLiner = '';
            console.log(summonerArray)
            for(let i=0;i<selectorArrayLang.length;i++){
              summonerNames=summonerArray.filter(word => word != selectorArrayLang[i]);
              summonerArray=summonerNames;
            }
            for(let i=0;i<summonerNames.length;i++){
              if(i==summonerNames.length-1){
                summonerNamesOneLiner+=summonerNames[i];
              }else{
                summonerNamesOneLiner+=summonerNames[i]+',';
              }
            }
            console.log(summonerNames)
            let tempUrl=''
            for(let x=0;x<summonerNames.length;x++){
              tempUrl=`https://www.leagueofgraphs.com/summoner/${this.regionSelected}/${summonerNames[x]}`
              console.log(tempUrl)
              window.open(tempUrl, '_blank')
            }
            tempUrl=`https://lan.op.gg/multisearch/${this.regionSelected}?summoners=${summonerNamesOneLiner}`
            console.log(tempUrl)
            window.open(tempUrl, '_blank')
    },
},
watch:{
    regionSelected(){
        if(this.regionSelected!='' && this.inputText!=''){
          this.isActive=false
          }
        else{
          this.isActive=true;
        }
    },
    inputText(){
      if(this.regionSelected!='' && this.inputText!=''){
          this.isActive=false
          }
        else{
          this.isActive=true;
        }
    }
}

}
</script>
