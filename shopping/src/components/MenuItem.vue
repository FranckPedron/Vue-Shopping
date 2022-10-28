<template>
  <div class="menu-item">
    <img class="menu-item__image" :src="image.source" :alt="image.alt" />
    <div>
      <h3>{{ name }}</h3>
      <p>Prix: {{ generatedPrice }} €</p>
      <p v-if="inStock">En stock</p>
      <p v-else>En rupture de stock</p>
      <div>
        <label for="add-item-quantity">Quantité : {{ quantity }}</label>
        <input v-model.number="qty" id="add-item-quantity" type="number" />
        <button @click="addToShoppingCart(qty)">
          Ajouter au panier
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MenuItem",
  props: ["addToShoppingCart", "image", "inStock", "price", "name", "quantity"],
  data() {
    return {
      qty: this.quantity,
      onSale: false
    }
  },
  computed: {
    generatedPrice() {
      if (this.onSale) {
        return (this.price * 0.9).toFixed(2);
      } else {
        return this.price;
      }
    }
  },
  beforeMount() {
    let date = new Date().getDate();
      if (date % 2 === 0) {
        this.onSale = true;
    }
  }
}
</script>

<style lang="scss">
  .menu-item {
    display: flex;
    width: 500px;
    justify-content: space-between;
    margin-bottom: 30px;

    &__image {
      max-width:300px;
    }
  }

</style>
