<template>
 <div class="hello">
    
<div class="d-flex flex-column flex-md-row align-items-center p-3 px-md-4 mb-3 bg-white border-bottom shadow-sm">
      <h5 class="my-0 mr-md-auto font-weight-normal">Rubens Carvalho</h5>
      <nav class="my-2 my-md-0 mr-md-3">
        <a class="p-2 text-dark" href="https://github.com/Rubensrvsc">GitHub</a>
        <a class="p-2 text-dark" href="https://www.linkedin.com/in/rubens-carvalho-892584120">Linkedin</a>
      </nav>
    </div>
<div id="imagem">
    <img alt="Vue logo" src="../assets/numero_binario.png">
    </div>

    <b-container fluid id="container_form">
     <b-form-input v-model = "titulo.numero" type="text"/>
      <b-button variant="outline-primary" class="button_form"
       @click="calculaNumeroParaDecimal"> Enviar numero</b-button>
    </b-container>
    <div id="apresentacao_numeros">
      <b-card class="tamanho_card"
      header="Apresentação dos resultados">
    <h4 class="numero_apresentacao">Número: {{titulo.numero}}</h4>
    <h3 class="numero_apresentacao"> Soma: {{titulo.soma}}</h3>
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

#imagem{
  margin-left: 38%;
}

#container_form{
  width: 50%;
  margin-top: 3%;
}

.numero_apresentacao{
  margin-left: 38%;
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
  margin-left: 35%;
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
