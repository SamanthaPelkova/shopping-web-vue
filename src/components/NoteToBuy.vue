<template>
  <div class="notes">
      <h2>Nákupní seznam</h2>
      <input type="text" placeholder="Nová mikina.." v-model="enteredItems"/>
      <button @click="addGoal">Přidat do seznamu</button>
      <p v-if="listItems.length === 0">Zatím zde nemáte žádné produkty, které potřebujete.</p>
      <ul v-else>
        <li v-for="(item, index) in listItems" :key="item">
          {{ item }} <button @click="removeGoal(index)">Smazat</button> <hr class="hr">
        </li>

      </ul>
  </div>
</template>

<script>

import cartItems from "@/components/CartItems.vue";
import {ref} from "vue";

export default {
  computed: {
    cartItems() {
      return cartItems
    }
  },

  setup(){
    const listItems = ref ([]);
    const enteredItems = ref('');

    const addGoal = () => {
      listItems.value.push(enteredItems.value)
      enteredItems.value = ''
    }

    const removeGoal = (goal) => {
      listItems.value.splice(goal, 1)
    }



    return{
      listItems,
      enteredItems,
      addGoal,
      removeGoal
    }


  }

}

</script>


<style>
.notes{
  position: absolute;
  float: left;
  width: 50%;
  border-radius: 20px;
  color: white;
  margin-top: 30px;
}

.notes input{
  border: 1px solid white;
  border-radius: 30px;
  font-size: 15px;
  padding: 5px 15px;
  width: 40%;
  background-color: white;
}

.notes button {
  border: 2px solid #966847;
  border-radius: 10px;
  background-color: #966847;
  margin-left: 10px;
  width: 40%;
  cursor: pointer;
  color: white;
  padding: 5px;
  font-size: 15px;
  transition: 0.4s;
}

.notes button:hover{
  background-color: #64452f;
  border: 2px solid #64452f;
  color: #af8465;
}
.notes ul li {
  list-style-type: none;
  font-size: 15px;
  text-align: start;
}

.notes ul li button{
  width: 30%;

}

.notes ul li .hr{
  width: 94%;
  text-align: start;
  margin-left: -15px;
}

</style>