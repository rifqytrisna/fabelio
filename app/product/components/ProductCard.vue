<template>
  <div>
    <v-card
      class="mx-auto product-card py-5 px-4"
      max-width="500"
      outlined
      elevation="3"
    >
      <div class="d-flex align-center justify-space-between">
        <h1>{{ product.name }}</h1>
        <span class="price">{{ product.price | priceIdr }}</span>
      </div>
      <p class="description">{{ product.description }}</p>
      <div class="style">
        <span v-for="style in product.furniture_style" :key="style">
          {{ style }},
        </span>
      </div>
      <p class="d-flex delivery-time">
        {{ product.delivery_time }} {{ deliveryTime }}
      </p>
    </v-card>
  </div>
</template>

<script>
export default {
  computed: {
    deliveryTime() {
      switch (this.product.delivery_time) {
        case '1':
          return 'day'
        default:
          return 'days'
      }
    }
  },
  props: { product: { type: Object, default: () => ({}) } }
}
</script>

<style lang="scss" scoped>
@import '~/app/designs/mixins/line_clamp.scss';

.product-card {
  border-radius: 8px;
}

.description {
  @include line-clamp(3);
  color: #646670;

  @include mq($until: tablet) {
    font-size: 14px;
  }
}

h1 {
  font-size: 16px;

  @include mq($from: tablet) {
    font-size: 24px;
  }
}

.price {
  color: #f46a00;
}

.style span {
  color: #627bdf;
}

.delivery-time {
  justify-content: flex-end;
  text-decoration: underline;
  color: #294bcf;
}
</style>
