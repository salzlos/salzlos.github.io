<template>
  <div id="product-list">
    <Button @clicked="$router.push({ path: '/shop/cart' })">
      <fa-icon icon="shopping-cart" size="lg" />
    </Button>
    <ShopItem
      v-for="product in products"
      :key="product.name"
      :product="product"
    />
  </div>
</template>

<script>
import ShopItem from './ShopItem';
import Button from './Button';

import { mapState } from 'vuex';

export default {
  name: 'ProductList',
  components: {
    ShopItem,
    Button,
  },
  computed: mapState({
    products: (state) => state.products.all,
  }),
};
</script>

<style lang="sass" scoped>
#product-list
  display: inline-flex
  position: relative
  width: 100%
  height: 80%
  flex-direction: row
  flex-wrap: wrap
  justify-content: center
  color: black
.button
  position: absolute
  top: 0px
  right: 0px
  margin-top: 10px
  margin-right: 10px
@media only screen and (max-width: 1000px)
  #product-list
    width: 100%
    padding-top: 50px
</style>
