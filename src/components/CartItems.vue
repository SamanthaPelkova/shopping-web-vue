<template>
  <div class="cart">
      <div class="header">
        <h2>Nákupní košík</h2>
      </div>
      <div v-if="cartItems.length === 0" class="basketIsEmpty">
        <p>Košík je prázdný</p>
      </div>
      <ul>
        <li v-for="(item) in cartItems" :key="item.id">
          <img :src="item.image" alt=""/>
          <button @click="item.quantity ++" >+</button>
          {{ item.quantity }} /ks
          <button @click="reduceQuantity(item)">-</button>
          {{ item.name }} - {{ item.quantity * item.price }} Kč
          <button class="removeFromBasket" @click="$emit('remove-item', item.id)">Odstranit</button>
        </li>
      </ul>
    <hr>
    <h2 class="totalPrice">Celková cena: </h2>
    <h1 class="totalPriceSum">{{ productsPrice }} Kč / {{ quantityOfProducts }} ks</h1>
    <div>

    </div>
  </div>
</template>

<script>
import {computed} from "vue";

export default {
  props: {
    cartItems: {
      type: Array,
      required: true
    }
  },
  emits: ['remove-item'],
  setup(props){
    const productsPrice = computed(() => {
      let totalPrice = 0
      props.cartItems.forEach((item)=>{
        totalPrice += item.price * item.quantity
      })
      return totalPrice
    })

    const quantityOfProducts = computed(() => {
      let totalQuantity = 0
      props.cartItems.forEach((product) => {
        totalQuantity += product.quantity
      })
      return totalQuantity
    })


    const reduceQuantity = (item) => {
      if (item.quantity > 1 ){
        item.quantity --
      }
    }

    return{
      reduceQuantity,
      quantityOfProducts,
      productsPrice,

    }

  }
};
</script>

<style scoped>
.cart {
  border: 0px solid #ccc;
  margin-top: 30px;
}

.cart ul li{
  list-style-type: none;
  font-size: 15px;
  padding-right: 15px;
}

*{
  background-color: #966847;
  color: white;
  border-radius: 20px;
}

.cart button {
  background-color: #2f82ff;
  color: black;
  margin-top: 15px;
  border: 2px solid #2f82ff;
  padding: 5px;
  font-size: 15px;
  border-radius: 10px 5px 10px 5px;
  cursor: pointer;
  transition: 0.4s;
}
.cart button:hover{
  background-color: blue;
  border: 2px solid blue;
  color: white;
  border-radius: 5px 10px 5px 10px;
}

.cart .removeFromBasket {
  background-color: red;
  border: #a40000;
  color: white;
  width: 50%;
}

.cart .removeFromBasket:hover{
  background-color: #a40000;
  border: #a40000;
  border-radius: 10px 20px 10px 20px;
}

.cart .basketIsEmpty p{
  color: black;
  text-align: center;
  width: 100%;
}

.cart ul li img {
  width: 6%;
  margin-bottom: -10px;
  margin-right: 7px;
}

.cart  hr{
  width: 90%;
}

.cart h3{
  width: 80%;
  text-align: right;
}

.cart p{
  width: 60%;
  font-size: 20px;
}

.cart .totalPrice {
  float: left;
  width: 60%;
  margin-top: 0px;
}

.cart .totalPriceSum {
  width: 90%;
  font-size: 20px;
}

</style>
