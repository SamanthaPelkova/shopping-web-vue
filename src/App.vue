<template>
  <div class="app">
    <h1 class="header">Malý e-shop</h1>
    <message-bar class="message" :cart-items="cartItems" :basket-messages="basketMessages" />
    <cart-items class="basket" :cart-items="cartItems" @remove-item="removeFromBasket"/>
    <div class="products">
      <product-item
          v-for="product in products"
          :key="product.id"
          :product="product"
          class="product-item"
          @add-to-basket="addToBasket(product, $event)"
      />
      <note-to-buy class="notesBlock"></note-to-buy>
    </div>
  </div>
</template>

<script>
import {ref} from 'vue';
import ProductItem from './components/ProductItem.vue';
import CartItems from './components/CartItems.vue';
import NoteToBuy from "@/components/NoteToBuy.vue";
import MessageBar from "@/components/MessageBar.vue";
import image1 from './images/modry-kabatek.webp';
import image2 from './images/orandzovy-kabatek.webp';
import image3 from './images/bily-kabatek.webp';
import image4 from './images/bezove-saty.webp';
import image5 from './images/modre saty.webp';
import image6 from './images/pomerancove saty.webp';
import image7 from './images/zelene saty.webp';
import image8 from './images/zlute saty.webp';

export default {
  components: {
    ProductItem,
    CartItems,
    NoteToBuy,
    MessageBar
  },
  setup() {
    const products = ref([
      {
        id: 1,
        name: 'Bright Blue Sako',
        price: 10899,
        image: image1,
        description: 'feoisfjoejf oejfoijiej jeofjjeiojf o ffsdfsf sdff iefjjfeslfmef efmefmkmfpem ekfmpempemf  epmfpmiejfijfe',
      },
      {
        id: 2,
        name: 'Bright Orange Sako',
        price: 11999,
        image: image2,
        description: 'feoisfjoejf oejfoefemfpkepfpem mfpemfpefm pekmfkp mpem fpm ekpmfm kp ijiej jeofjjeiojf oiefjjiejfijfe',
      },
      {
        id: 3,
        name: 'Open White Sako',
        price: 10999,
        image: image3,
        description: 'feoisfjoejf oejfoijiej jeofjjfepfk fekfm ekfmokmef oefmoekmff meifnifmi epkfmkepmf meiojf oiefjjiejfijfe',
      },
      {
        id: 4,
        name: 'Béžové společenské šaty',
        price: 999,
        image: image4,
        description: 'feoisfjoejf oejfoijiej jeofjjfepfk fekfm ekfmokmef oefmoekmff meifnifmi epkfmkepmf meiojf oiefjjiejfijfe',
      },
      {
        id: 5,
        name: 'Clear blue šaty',
        price: 1199,
        image: image5,
        description: 'feoisfjoejf oejfoijiej jeofjjfepfk fekfm ekfmokmef oefmoekmff meifnifmi epkfmkepmf meiojf oiefjjiejfijfe',
      },
      {
        id: 6,
        name: 'Pomerančové šaty',
        price: 299,
        image: image6,
        description: 'feoisfjoejf oejfoijiej jeofjjfepfk fekfm ekfmokmef oefmoekmff meifnifmi epkfmkepmf meiojf oiefjjiejfijfe',
      },
      {
        id: 7,
        name: 'Boho šaty',
        price: 599,
        image: image7,
        description: 'feoisfjoejf oejfoijiej jeofjjfepfk fekfm ekfmokmef oefmoekmff meifnifmi epkfmkepmf meiojf oiefjjiejfijfe',
      },
      {
        id: 8,
        name: 'Hořčicové šaty',
        price: 899,
        image: image8,
        description: 'feoisfjoejf oejfoijiej jeofjjfepfk fekfm ekfmokmef oefmoekmff meifnifmi epkfmkepmf meiojf oiefjjiejfijfe',
      },
    ]);

    const basketMessages = ref([])
    const messageCounter = ref(0)

    const cartItems = ref([])
    const addToBasket = (product, quantity) => {
      const existingProduct = cartItems.value.find( (p) => p.id === product.id)
      if (existingProduct){
        existingProduct.quantity += quantity
        addMessage('Produkt přidán')
        return
      }
      const cartProduct = { ...product, quantity }
      cartItems.value.push(cartProduct)
      addMessage('Produkt přidán')
    }

    const removeFromBasket = (productId) => {
      cartItems.value = cartItems.value.filter(item => item.id !== productId)
      addMessage('Produkt odebrán')
    };

    const addMessage = (message) => {
      const idOfNewMessage = messageCounter.value
      basketMessages.value.push({
        id: idOfNewMessage,
        text: message
      })
      messageCounter.value++

      setTimeout(() => {
        basketMessages.value = basketMessages.value.filter(m => m.id !== idOfNewMessage)
      }, 2000)
    }

    return {
      products,
      basketMessages,
      cartItems,
      removeFromBasket,
      addToBasket,
      MessageBar
    };
  },
};
</script>

<style>
body{
  background-color: rgba(0, 0, 0, 0.91);
}

.app {
  text-align: center;
  margin-top: 20px;
}

.app .header {
  background-color: rgba(90, 110, 241, 0.84);
  border-radius: 30px;
}

.products {
  display: flex;
  justify-content: center;
  background-color: rgba(0, 34, 255, 0.35);
  border-radius: 20px;
  width: 75%;
  flex-wrap: wrap;
}

.product-item{
  width: calc(25% - 50px);
}

.notesBlock{
  background-color: #5d5a55;
  width: 20%;
  position: fixed;
  margin-left: 1900px;
  margin-top: 30%;
}

.basket{
  width: 20%;
  position: fixed;
  margin-left: 1480px;
}
</style>
