<template>
  <div>
    <h1 class="messageProductsInBasket" v-if="calcNumberOfProducts === 0">Žádný produkt v košíku</h1>
    <h1 v-if="calcNumberOfProducts > 0" class="productsInBasket">{{ calcNumberOfProducts }}: v košíku</h1>
    <p v-for="message in basketMessages" :key="message.id" class="message-text">{{ message.text }}</p>
  </div>
</template>

<script>

import {computed} from "vue";

export default {
  props:{
    basketMessages:{
      type: Array,
      required: true
    },
    cartItems:{
      type: Array,
      required: true
    },
  },
  setup(props){
    const calcNumberOfProducts = computed(() => {
      let productsCount = 0

     props.cartItems.forEach((product) => {
       productsCount += product.quantity
      })

      return productsCount
    })



    return{
      calcNumberOfProducts
    }

}


}

</script>

<style>

.productsInBasket {
  background-color: rgba(47, 130, 255, 0.58);
  color: rgba(0, 0, 0, 0.66);
  position: fixed;
  display: flex;
  padding-left: 30px;
  font-size: 30px;
  border-radius: 30px;
  margin-top: -57.5px;
  width: 20%;
  margin-left: 1650px;
}
.messageProductsInBasket {
  background-color: rgba(0, 0, 0, 0.69);
  color: rgba(176, 160, 160, 0.66);
  position: fixed;
  display: flex;
  padding-left: 20px;
  padding-top: 6px;
  padding-bottom: 6px;
  font-size: 20px;
  border-radius: 30px;
  margin-top: -57.5px;
  width: 20%;
  margin-left: 1650px;
}

.message-text {
  background-color: rgba(62, 211, 70, 0.69);
  color: rgba(0, 0, 0, 0.66);
  position: fixed;
  display: flex;
  padding-left: 42px;
  padding-top: 6px;
  padding-bottom: 6px;
  font-size: 15px;
  border-radius: 30px;
  margin-top: -20.5px;
  width: 20%;
  margin-left: 1750px;
}



</style>