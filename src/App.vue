<script setup>


</script>

<template>
 <div class="contenedor">
  <div class="header">
   <img src="" alt="">
  <select name="tipobatalla" id="batalla">
     <option value="total">TOTAL</option>
    <option value="hp">HP</option>
    <option value="ataque">ATAQUE</option>
    <option value="defensa">DEFENSA</option>
    <option value="ataquesp">ATAQUE ESPECIAL</option>
    <option value="defensasp">DEFENSA ESPECIAL</option>
    <option value="velocidad">SPEED</option>
  </select> 
  <button id="iniciar" @click="batallapokemon()">INICIAR</button>
  </div>
  <div class="cuerpo">

  </div>
 </div>
</template>

<style scoped>
.container{
  display: flex;
}
.header{
  padding: 0px;
  margin: 0%;
  display: flex;
  
  
  background-size: cover;
 
  justify-content: center;
  flex-direction: column;
}
</style>
