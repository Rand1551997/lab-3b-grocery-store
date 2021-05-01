<template>
<div class="wrapper">
<div v-if = "this.$root.$data.total == 0">
<p>Cart is Empty</p>
</div>
  <div class="products" v-else>
    <div class="product" v-for="product in productsCart" :key="product.id">
      <div class="info">
        <h1>{{product.name}}</h1>
        <p>{{product.country}}</p>
      </div>
      <div class="image">
        <img :src="'/images/products/'+product.image">
      </div>
      {{product.quantity}}
      <div class="price">
        <h2>{{product.price}}</h2>
        <button class="auto" v-on:click="clickFunc(product.id)">Remove Item</button>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'Cart',
  props: {
  },
  methods: {
    clickFunc(id){
      let itemID = -1;
      for(let i = 0; i < this.$root.$data.cart.length; i++){
        if(id == this.$root.$data.cart[i].id){
          itemID = i;
        }
      }
      let numberRemove = this.$root.$data.cart[itemID].quantity;
      this.$root.$data.cart = this.$root.$data.cart.filter(eachItem=> eachItem.id != id);
      this.$root.$data.total-= numberRemove;
      console.log(this.$root.$data.cart[itemID]);
    }

  },
  computed: {
    productsCart() {
      return this.$root.$data.cart;
    }
  }
}
</script>

<style scoped>
.wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
}

.products {
  margin-top: 20px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.product {
  margin: 10px;
  margin-top: 50px;
  width: 200px;
}

.product img {
  border: 2px solid #333;
  height: 250px;
  width: 200px;
  object-fit: cover;
}

.product .image {
  display: flex;
  justify-content: center;
  margin-bottom: 5px;
}

.info {
  background: #F2921D;
  color: #000;
  padding: 10px 30px;
  height: 80px;
}

.info h1 {
  font-size: 16px;
}

.info h2 {
  font-size: 14px;
}

.info p {
  margin: 0px;
  font-size: 10px;
}


.price {
  display: flex;
}

button {
  height: 50px;
  background: #000;
  color: white;
  border: none;
}

.auto {
  margin-left: auto;
}
</style>
