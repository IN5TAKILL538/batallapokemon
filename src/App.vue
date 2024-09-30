<script setup>
import axios from "axios";
import { ref } from "vue";

let nombre = ref("");
let image = ref("");
let numpokedex = ref("");
let stats = ref("");

let nombre2 = ref("");
let image2 = ref("");
let numpokedex2 = ref("");
let stats2 = ref("");

let numeros1 = ref([]);
let numeros2 = ref([]);
let numi = ref(0); // Cambia a ref
let i = ref(0); // Cambia a ref

let statshp = ref("");
let statsatk = ref("");
let statsdf = ref("");
let statsatksp = ref("");
let statsdfsp = ref("");
let statsspeed = ref("");

let statshp2 = ref("");
let statsatk2 = ref("");
let statsdf2 = ref("");
let statsatksp2 = ref("");
let statsdfsp2 = ref("");
let statsspeed2 = ref("");

function numerospokedex() {
  numeros1.value = []; // Limpia el arreglo antes de llenarlo
  numeros2.value = [];

  for (let j = 0; j < numi.value; j++) {
    const numeroAleatorio1 = Math.floor(Math.random() * 1000) + 1;
    numeros1.value.push(numeroAleatorio1);
    const numeroAleatorio2 = Math.floor(Math.random() * 1000) + 1;
    numeros2.value.push(numeroAleatorio2);
    console.log(numeroAleatorio1);
    console.log(numeroAleatorio2);
  }
  
}

async function listarPokemon() {
  const boton = document.getElementById("iniciar");
  document.getElementById("nextcombat").style.display="block"
  boton.disabled = true;
  // Obtener el número de Pokémon a mostrar
  numi.value = parseInt(document.getElementById("numpokemon").value); // Asegúrate de que numi sea un número
  console.log(numi.value);
  
  // Llenar los números aleatorios
  numerospokedex();

  // Asegúrate de que i esté dentro del rango
  if (i.value < numi.value) {
    let url1 = 'https://pokeapi.co/api/v2/pokemon/' + numeros1.value[i.value];
    let url2 = 'https://pokeapi.co/api/v2/pokemon/' + numeros2.value[i.value];
    try {
      let { data } = await axios.get(url1);
      console.log(data);

      nombre.value = data.name;
      numpokedex.value = data.id;
      image.value = data.sprites.front_default;
      statshp.value = data.stats[0].base_stat;
      statsatk.value = data.stats[1].base_stat;
      statsdf.value = data.stats[2].base_stat;
      statsatksp.value = data.stats[3].base_stat;
      statsdfsp.value = data.stats[4].base_stat;
      statsspeed.value = data.stats[5].base_stat;
      stats.value = statsatk.value + statsdf.value + statsatksp.value + statsdfsp.value + statsspeed.value;

      let { data: data2 } = await axios.get(url2);
      nombre2.value = data2.name;
      numpokedex2.value = data2.id;
      image2.value = data2.sprites.front_default;
      statshp2.value = data2.stats[0].base_stat;
      statsatk2.value = data2.stats[1].base_stat;
      statsdf2.value = data2.stats[2].base_stat;
      statsatksp2.value = data2.stats[3].base_stat;
      statsdfsp2.value = data2.stats[4].base_stat;
      statsspeed2.value = data2.stats[5].base_stat;
      stats2.value = statsatk2.value + statsdf2.value + statsatksp2.value + statsdfsp2.value + statsspeed2.value;

      i.value++; // Incrementa i después de obtener los datos
      
    } catch (error) {
      alert("Ocurrió un error al obtener los datos. Por favor, inténtalo de nuevo.");
    }
  } else {
    
  }
  
}
function compararEstadisticas() {
  const tipoBatalla = document.getElementById("batalla").value;

  let statPokemon1, statPokemon2;
  let ganador;

  switch (tipoBatalla) {
    case "total":
    statPokemon1 = parseInt(stats.value);
    statPokemon2 = parseInt(stats2.value);
    break;
    case "hp":
      statPokemon1 = parseInt(statshp.value);
      statPokemon2 = parseInt(statshp2.value);
      break;
    case "attack":
      statPokemon1 = parseInt(statsatk.value);
      statPokemon2 = parseInt(statsatk2.value);
      break;
    case "defense":
      statPokemon1 = parseInt(statsdf.value);
      statPokemon2 = parseInt(statsdf2.value);
      break;
    case "special-attack":
      statPokemon1 = parseInt(statsatksp.value);
      statPokemon2 = parseInt(statsatksp2.value);
      break;
    case "special-defense":
      statPokemon1 = parseInt(statsdfsp.value);
      statPokemon2 = parseInt(statsdfsp2.value);
      break;
    case "speed":
      statPokemon1 = parseInt(statsspeed.value);
      statPokemon2 = parseInt(statsspeed2.value);
      break;
    default:
      return; // Si no hay selección válida, salir
  }

  if (statPokemon1 > statPokemon2) {
    ganador = `${nombre.value} gana con ${statPokemon1} ${tipoBatalla}!`;
  } else if (statPokemon1 < statPokemon2) {
    ganador = `${nombre2.value} gana con ${statPokemon2} ${tipoBatalla}!`;
  } else {
    ganador = "Es un empate!";
  }

  alert(ganador); // Muestra el resultado en un alert
}
</script>

<template>
  <div class="contenedor">
    <div class="header">
      <img src="" alt="">
      <select name="numpokemon" id="numpokemon">
        <option value="1">1</option>
        <option value="2">2</option>
        <option value="3">3</option>
        <option value="4">4</option>
        <option value="5">5</option>
        <option value="6">6</option>
      </select>
      <select name="tipobatalla" id="batalla">
        <option value="total">TOTAL</option>
        <option value="hp">HP</option>
        <option value="attack">ATAQUE</option>
        <option value="defense">DEFENSA</option>
        <option value="special-attack">ATAQUE ESPECIAL</option>
        <option value="special-defense">DEFENSA ESPECIAL</option>
        <option value="speed">VELOCIDAD</option>
      </select>
      <button id="iniciar" @click="listarPokemon()">INICIAR</button>
    </div>
    <div class="cuerpo">
      <div class="pokemon" id="poke1">
        <div id="name1">{{ nombre }}</div>
        <img :src="image" alt="" class="imgpoke">
      </div>
      <img src="https://pm1.aminoapps.com/6451/08ef2400e95ad4f34b3f61be0bdf4f66927a6be0_00.jpg" alt="">
      <div class="pokemon" id="poke2">
        <div id="name2">{{ nombre2 }}</div>
        <img :src="image2" alt="" class="imgpoke">
      </div>
     
    </div>
    <div class="btnnext"><button id="nextcombat" @click="listarPokemon()">Siguiente Combate</button></div>
  </div>
</template>

<style>
.container {
  display: flex;
}

.cuerpo {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}

.header {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.imgpoke {
  width: 260px;
  height: 260px;
}

#numpokemon {
  width: 100px;
  height: 20px;
}

#batalla {
  width: 100px;
  height: 20px;
}
#nextcombat{
  display: none;
  
}
.btnnext{
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>