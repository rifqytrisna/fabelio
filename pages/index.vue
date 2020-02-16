<template>
  <v-container>
    <div class="filter-wrapper">
      <v-col sm="6" class="ml-md-3">
        <v-text-field
          v-model="searchKey"
          placeholder="Search Furniture"
          color="white"
          dark
        ></v-text-field>
      </v-col>
      <v-row class="mx-3">
        <v-col cols="12" sm="6">
          <v-select
            v-model="styleKey"
            :items="furnitureStyles"
            :value="furnitureStyles"
            label="Furniture Style"
            multiple
            solo
          ></v-select>
        </v-col>
        <v-col cols="12" sm="6">
          <v-select
            v-model="deliveryKey"
            :items="deliveryItem"
            :value="deliveryItem"
            label="Delivery Time"
            multiple
            solo
          ></v-select>
        </v-col>
      </v-row>
    </div>

    <v-row class="mx-1" style="border: solid 1px black;">
      <v-col v-for="product in filteredProduct" :key="product.name" md="6">
        <ProductCard :product="product"></ProductCard>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import ProductCard from '~/app/product/components/ProductCard'

export default {
  components: {
    ProductCard
  },
  async asyncData(context) {
    const response = await context.$axios.get(
      'http://www.mocky.io/v2/5c9105cb330000112b649af8'
    )

    const productList = response.data.products

    const furnitureStyles = response.data.furniture_styles

    return {
      productList,
      furnitureStyles
    }
  },
  data: () => ({
    searchKey: '',
    deliveryKey: [],
    styleKey: [],
    deliveryItem: ['1', '2', '7', '12', '14', '28']
  }),
  computed: {
    filteredProduct() {
      let filterProduct = this.productList

      if (this.searchKey !== '') {
        filterProduct = filterProduct.filter((product) => {
          return product.name
            .toLowerCase()
            .includes(this.searchKey.toLowerCase())
        })
      }

      if (this.deliveryKey.length > 0) {
        filterProduct = filterProduct.filter((product) => {
          return this.deliveryKey.includes(product.delivery_time)
        })
      }

      if (this.styleKey.length > 0) {
        filterProduct = filterProduct.filter((product) => {
          return this.styleKey.includes()
        })
      }

      return filterProduct
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~/app/designs/mixins/_mq.scss';

.filter-wrapper {
  background-color: #1f47e4;
  margin: 0 3px;
}

::v-deep .theme--light.v-input input,
.v-input input::placeholder {
  color: #ffff !important;
  font-weight: 500;
}
</style>
