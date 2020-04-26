<template>
  <div id="app" class="flex justify-center">
    <div
      class="grid grid-cols-4 font-sans antialiased w-80 text-xl text-center text-gray-300 bg-gray-910 rounded-lg mt-32 shadow-xl"
    >
      <div value="123,456" class="flex items-end col-span-4 h-48 bg-gray-920 rounded-t-lg">
        <div
          class="bg-gray-920 w-full focus:outline-none text-right text-white text-5xl tracking-wide mr-2"
        >{{ valorCorrente || '0' }}</div>
      </div>
      <div @click="limpar" class="btn border-gray-905">AC</div>
      <div @click="porcentagem" class="btn border-gray-905">%</div>
      <div @click="backspace" class="btn border-gray-905">
        <span class="material-icons-outlined text-lg align-middle">backspace</span>
      </div>
      <div @click="dividir" class="btn border-gray-905 text-blue-500">÷</div>
      <div @click="juntarNumeros('7')" class="btn border-gray-905">7</div>
      <div @click="juntarNumeros('8')" class="btn border-gray-905">8</div>
      <div @click="juntarNumeros('9')" class="btn border-gray-905">9</div>
      <div @click="multiplicar" class="btn border-gray-905 text-blue-500">x</div>
      <div @click="juntarNumeros('4')" class="btn border-gray-905">4</div>
      <div @click="juntarNumeros('5')" class="btn border-gray-905">5</div>
      <div @click="juntarNumeros('6')" class="btn border-gray-905">6</div>
      <div @click="subtrair" class="btn border-gray-905 text-blue-500">-</div>
      <div @click="juntarNumeros('1')" class="btn border-gray-905">1</div>
      <div @click="juntarNumeros('2')" class="btn border-gray-905">2</div>
      <div @click="juntarNumeros('3')" class="btn border-gray-905">3</div>
      <div @click="somar" class="btn border-gray-905 text-blue-500">+</div>
      <div @click="juntarNumeros('0')" class="col-span-2 btn border-gray-905 rounded-bl-lg">0</div>
      <div @click="ponto" class="btn border-gray-905">.</div>
      <div @click="resultado" class="btn border-blue-500 bg-blue-500 hover:bg-blue-400 hover:text-b rounded-br-lg">=</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      valorCorrente: "",
      numeroAnterior: null,
      operador: null,
      operadorClicado: true
    };
  },
  methods: {
    limpar() {
      this.valorCorrente = "";
    },

    setarValor() {
      this.numeroAnterior = this.valorCorrente;
      this.operadorClicado = true;
    },

    backspace() {
      this.valorCorrente = this.valorCorrente.slice(0, -1);
    },

    juntarNumeros(numero) {
      if (this.operadorClicado) {
        this.valorCorrente = "";
        this.operadorClicado = false;
      }

      this.valorCorrente = `${this.valorCorrente}${numero}`;
    },
    ponto() {
      /**
       * Inclui o ponto flutuante na variavel valorCorrente
       *
       *  String.prototype.indexOf('VALOR ESPECIFICADO')
       *  é usada para buscar o valor indice do 'VALOR ESPECIFICADO dentro da String.
       *  Caso não seja encontrado retorna -1.
       *
       *  Na logica, CASO dentro da index da string 'this.valorCorrente'
       *  não tenha o valor '.' o metodo retorna -1 nesse caso o if será false e adcionará na variavel
       *  this.valorCorrete o caractere '.'
       *
       */
      if (this.valorCorrente.indexOf(".") == -1) {
        this.juntarNumeros(".");
      }
    },
    somar() {
      this.operador = (num1, num2) => num1 + num2;
      this.setarValor();
    },
    subtrair() {
      this.operador = (num1, num2) => num1 - num2;
      this.setarValor();
    },
    multiplicar() {
      this.operador = (num1, num2) => num1 * num2;
      this.setarValor();
    },
    dividir() {
      this.operador = (num1, num2) => num1 / num2;
      this.setarValor();
    },
    porcentagem() {
      if (this.valorCorrente != '0') {
        this.valorCorrente = `${parseFloat(this.valorCorrente) / 100}`;  
      }
      
    },
    resultado(){
      this.valorCorrente = `${this.operador(
        parseFloat(this.numeroAnterior),
        parseFloat(this.valorCorrente),
      )}`;
      this.numeroAnterior = null;
      console.log(this.valorCorrente)
    },
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/icon?family=Material+Icons+Outlined");

.btn {
  @apply py-4 border-t border-r border-b;
}
.btn:hover {
  @apply  bg-gray-905 
}
</style>