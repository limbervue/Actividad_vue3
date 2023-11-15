<template>
  <h2>Cena {{ counter+1 }}
    con el rey godo {{ rey }}
  </h2>
  <h3 class="price">Precio: ${{ products[counter].price }}</h3>
  <div v-if="products[counter].weekend" class="weekend days">
	(just weekend)
  </div>
  <div v-else class="everyday days">
	(everyday)
  </div>
  <div v-if="products[counter].price<100" class="oferta">
	<div>
		Ahora un 10% dto: 
		${{ newPrice }}
	</div>
	<img src="/oferta.jpg" alt="">
  </div>
  <div>
	<img :src="imagen" alt="">
  </div>
  
  <div>
    <button @click="next()">next ({{ counter+1 }}/{{ total }})</button>
  </div>
  
</template>

<script setup>
  import { products } from './data.js';
  import {ref, computed} from "vue";
  const counter = ref(0);
  const total = products.length;
  const ruta = "https://www.html6.es/img/rey_";

  const next=()=>{
    counter.value++
    if(counter.value >= total){
       counter.value = 0;
    }
  }
  const rey = computed(()=>{
    const name =  products[counter.value].name.toLowerCase();
    return name.substring(0,1).toUpperCase() + name.substring(1);
  })

  const imagen = computed(()=>{
    return `${ruta}${products[counter.value].name.toLowerCase()}.png`
  })

  const newPrice = computed(()=>{
	const diez = (products[counter.value].price * 10)/100
	return  Number(products[counter.value].price - diez).toFixed(2)
  })
</script>

<style scoped>
	.everyday{
		background-color: green;
	}
	.weekend{
		background-color: red;
	}
	.days{
		border-radius: 4px;
		padding: 4px 17px;
		color: white;
		font-size: 0.9em;
		margin: 5px 0 10px;
		display: inline-block;
	}
	.oferta img{
		width: 65px;
		margin: 10px 3px;
	}
</style>