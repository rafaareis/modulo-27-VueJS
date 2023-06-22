<script setup>
import { reactive } from 'vue';

  const nome = "Courtney LaPlante"

  const meuObj = {
    nome: 'Rafael de Alvarenga Reis',
    filmeFavorito: 'Resgate'
  }

  function dizOla() {
    return `${nome} diz oi`;
  }

  const imgSpiritbox = "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT2ZCMLrXZbE1EGEn-zB_dwThU15r4QD_wktQ&usqp=CAU";
  const imgRoyalBlood = "https://th.bing.com/th/id/OIP.vaaC4t0YCiUi09xh2UXQZAHaE8?w=299&h=199&c=7&r=0&o=5&pid=1.7";

  const botaoEstaDesabilitado = true;

  const gostaDeSpiritbox = false;
  const gostaDeRoyalBlood = false;

  const estado = reactive({
    contador: 0,
    email: '',
    saldo: 5000,
    transferindo: 0
  })

  function incrementar() {
    estado.contador++ ;
  }

  function decrementar() {
    estado.contador-- ;
  }

  function alteraEmail(evento) {
    estado.email = evento.target.value;
  }

  function mostraSaldoFuturo() {
    const {saldo, transferindo } = estado;
    return saldo - transferindo;
  }

  function validaValorTransferencia() {
    const {saldo, transferindo } = estado;
    return saldo >= transferindo;
  }

  const bandas = reactive({
    nomesDeBandas: ['Jinjer', 'Baroness', 'Spiritbox', 'Royal Blood', 'Larkin Poe', 'Extreme', 'Foo Fighters', 'Metallica'],
    inserirNome: '',
  })

  function cadastrarNome() {
    if (bandas.inserirNome.length >= 3) {
      bandas.nomesDeBandas.push(bandas.inserirNome)
    } else {
      alert(`Digite mais caracteres.`)
    }
  } 

</script>



<template>
    <h1>Olá {{ nome }}</h1>
    <h2>Olá {{ meuObj.nome }}. Seu filme favorito é {{ meuObj.filmeFavorito }}</h2>
    <h2>{{ dizOla() }}</h2>

    <img v-if="gostaDeSpiritbox"  :src="imgSpiritbox" alt="">
    <img v-else-if="gostaDeRoyalBlood" :src="imgRoyalBlood" alt="">
    <h2 v-else>Não gosta de nenhuma das duas bandas.</h2>

    <button :disabled="botaoEstaDesabilitado">Enviar mensagem</button>
    <br />
    <hr />

    {{ estado.contador }}

    <button @click="incrementar" type="button">+</button>
    <button @click="decrementar"  type="button">-</button>

    <br />
    <hr />

    {{ estado.email }}
    <input type="email" @keyup="alteraEmail">

    <br />
    <hr />

    Saldo: {{ estado.saldo }} <br />
    Transferindo: {{ estado.transferindo }} <br />
    Saldo depois da Transferência: {{ mostraSaldoFuturo() }} <br />

    <input class="campo" :class="{ invalido: !validaValorTransferencia() }" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir">
    <button v-if="validaValorTransferencia()">Transferir</button>
    <span v-else>Valor maior que o saldo</span>

    <br />
    <hr />

    <ul>
      <li v-for="nome in bandas.nomesDeBandas">
        {{ nome }}
      </li>
    </ul>
    <input @keyup="evento => bandas.inserirNome = evento.target.value" type="text" placeholder="Digite um novo nome">
    <button @click="cadastrarNome()" type="button">Cadastrar nome</button>

</template>

<style scoped>

  img {
    max-width: 200px;
  }

  .invalido {
    outline-color: red;
    border-color: red;
  }

  .campo{
    border: 2px solid #000;
  }

</style>
