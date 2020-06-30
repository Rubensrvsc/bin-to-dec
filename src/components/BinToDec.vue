<template>
 <div class="hello">
    

    <b-container fluid id="container_form">
     <b-form-input v-model = "titulo.numero" type="text"/>
      <b-button variant="outline-primary" class="button_form"
       @click="calculaNumeroParaDecimal"> Enviar numero</b-button>
    </b-container>
    <div id="apresentacao_numeros">
      <b-card class="tamanho_card"
      header="Apresentação dos resultados">
    <h4>Numero: {{titulo.numero}}</h4>
    <h3> Soma: {{titulo.soma}}</h3>
      </b-card>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BinToDec',
  props: {
    msg: String,
    //title: String,
    nome: String,
    numero: Number
  },

  data(){

    return {
      titulo: {
        title: '',
        numero: '',
        verifica_numero: false,
        soma: 0,
      },
      controle: {
        cont: 0,
        acumula_soma: 0
      }
    }
  },

  methods:{
    enviarNome(){
      this.nome=this.titulo.title;
    },

    calculaNumeroParaDecimal(){
      if(this.titulo.numero.length > 8){
        alert("Numero maior que 8 digitos")
        this.titulo.verifica_numero = true;
        this.titulo.numero='';
      }
      else{
        for(let i=0;i<this.titulo.numero.length;i++){
          if (this.titulo.numero[i] != '0' && this.titulo.numero[i] != '1'){
            alert("existe numero não binário");
            this.titulo.verifica_numero = true;
            this.titulo.numero='';
            
          }
          //console.log(this.titulo.numero[i]);
        }
      }

        if(this.titulo.verifica_numero === false){
          console.log("entrou");
          for(let i = this.titulo.numero.length - 1; i>=0;i--){
            this.controle.acumula_soma += Number(this.titulo.numero[i])  * (2 ** this.controle.cont);
            this.controle.cont++;
            console.log(this.controle.cont);
          }
          this.controle.cont=0;
          this.titulo.soma = this.controle.acumula_soma;
          console.log("Soma: "+this.titulo.soma);
          this.controle.acumula_soma=0;
        }

        this.titulo.verifica_numero = false;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#container_form{
  width: 50%;
}

.tamanho_card{
  margin-left: 25%;
  width: 50%;
}

#apresentacao_numeros{
  margin-top: 3%;
}

#distancia_link{
  padding: 3%;
}

.button_form{
  margin-top: 3%;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
