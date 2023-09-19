<template>
  <div class="product">
      <h3>{{ product.name }}</h3>
      <p>Cena: {{ product.price}} Kč</p>
      <img :src="product.image" alt=""/>
      <p>{{product.description}}</p>
      <button @click="increaseQuantity">+</button>
      <input v-model="quantity" min="1" @input="updateQuantity" />
      <button class="plus&minus" @click="decreaseQuantity">-</button>
      <button class="buy" @click="$emit('add-to-basket', quantity)"> Koupit </button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  props: {
    product: {
      type: Object,
      required: true
    },
  },
  emits: ['add-to-basket'],
  setup() {
    const quantity = ref(1);

    const updateQuantity = (event) => {
      quantity.value = parseInt(event.target.value);
    };

    const increaseQuantity = () => {
      quantity.value = (quantity.value +1)
    };


    const decreaseQuantity = () => {
      if (quantity.value >1) {
          quantity.value = (quantity.value -1)
      }

    }

    return {
      quantity,
      updateQuantity,
      increaseQuantity,
      decreaseQuantity,
    };
  },
};
</script>

<style scoped>
.product {
  border: 4px solid rgba(90, 110, 241, 0.84);
  border-radius: 40px;
  padding: 10px;
  margin: 10px;
  background-color: rgba(0, 0, 0, 0.69);
}

.product h3{
  background-color: rgba(0, 0, 0, 0.69);
  color: white;
  font-size: 20px;
}

.product p{
  background-color: rgba(0, 0, 0, 0.69);
  color: rgba(90, 110, 241, 0.84);
  font-family: Arial cursive;

}

.product img{
  width: 100%;
  border-radius: 20px;

}

.product input{
  background-color: white;
  color: black;
  border: 3px solid white;
  border-radius: 10px;
  width: 10%;
  text-align: center;
  font-size: 15px;
  padding: 10px;
}

.product button{
  background-color: #2f82ff;
  margin: 10px;
  color: white;
  border: 2px solid #2f82ff;
  padding: 5px;
  font-size: 25px;
  border-radius: 10px 5px 10px 5px;
  cursor: pointer;
  transition: 0.4s;
}

.product button:hover{
  background-color: blue;
  border: 2px solid blue;
  color: white;
}

.product .buy {
  background-color: rgba(173, 255, 47, 0.76);
  border: 2px solid rgba(173, 255, 47, 0.76);
  width: 40%;
  font-size: 25px;
}

.product .buy:hover {
  background-color: #966847;
  border: 2px solid #966847;
}

</style>
