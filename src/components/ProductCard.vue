<template>
  <div class="card-wrapper">
    <div class="product-details">
      <div>
        <img
          v-if="product.image"
          :src="product.image"
          :alt="product.name"
          class="product-image"
        />
        <img
          v-else
          src="@/assets/images/default-image.png"
          :alt="product.name"
          class="product-image"
        />
      </div>
      <div
        class="product-status"
        :style="{ 'background-color': product.status }"
      ></div>

      <h4 class="product-name">{{ product.name }}</h4>
    </div>
    <div class="date-dropdown">
        <h4 class="product-name" v-if="product.date">{{ formateDate }}</h4>
        <img src="@/assets/icons/arrow-down.svg" alt="arrow-down" />
    </div>
  </div>
</template>
<script>
export default {
  name: "ProductCard",
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  computed: {
    formateDate() {
        return new Date(this.product.date).toLocaleDateString()
    }
  }
};
</script>
<style scoped>
.card-wrapper {
  display: flex;
  justify-content: space-between;
  padding: 12px 0;
  align-items: center;
  border-bottom: 1px solid #f0f2f4;
}

.card-wrapper .product-details {
  display: flex;
  align-items: center;
  column-gap: 12px;
}

.card-wrapper .product-image {
  height: 24px;
  width: 24px;
  border-radius: 2px;
  object-fit: cover;
  object-position: center;
}

.card-wrapper .product-status {
  width: 9.33px;
  height: 9.33px;
  background-color: red;
  border-radius: 100px;
}

.card-wrapper .product-name {
  font-family: "Inter", sans-serif;
  font-size: 14px;
  line-height: 22px;
  font-weight: 400;
  color: #252526;
  max-width: 183px;
}

.date-dropdown {
    display: flex;
    align-items: center;
    column-gap: 12px;
}
</style>
