<template>
  <div class="container">
    <HeaderMenu />

    <div class="content">
      <InputForm
        key="search"
        placeholder="Find a Product"
        @submit-data="setSearchKey"
      />
      <InputForm
        key="addProduct"
        placeholder="Product name"
        @submit-data="addProduct"
      >
        <button type="submit" class="add-form-button">Add Product</button>
      </InputForm>

      <div class="products-container">
        <ProductCard
          v-for="(product, index) in pageproducts"
          :key="index"
          :product="product"
        />
      </div>
    </div>

    <FooterMenu
      :current-page="currentPage"
      :total="total"
      :total-pages="totalPages"
      @change-page="currentPage = $event"
      @change-sort-order="changeSortOrder"
    />
  </div>
</template>

<script>
import HeaderMenu from "./components/HeaderMenu.vue";
import InputForm from "./components/InputForm.vue";
import ProductCard from "./components/ProductCard.vue";
import products from "@/assets/data.js";
import FooterMenu from "./components/FooterMenu.vue";

export default {
  name: "App",
  components: { HeaderMenu, InputForm, ProductCard, FooterMenu },
  data() {
    return {
      products: [...products],
      currentPage: 1,
      perPage: 10,
      searchKey: "",
      sortOrder: null,
    };
  },

  computed: {
    filteredProducts() {
      const tempFilteredProducts = this.products.filter((product) =>
        product.name.toLowerCase().includes(this.searchKey)
      );
      if (this.sortOrder) {
        return tempFilteredProducts.sort((a, b) => {
          const aName = a.name.toLocaleLowerCase();
          const bName = b.name.toLocaleLowerCase();
          if (this.sortOrder === "Asc") {
            if (aName > bName) {
              return 1;
            }
            if (aName < bName) {
              return -1;
            }
          } else {
            if (aName > bName) {
              return -1;
            }
            if (aName < bName) {
              return 1;
            }
          }

          return 0;
        });
      }
      return tempFilteredProducts;
    },
    from() {
      return (this.currentPage - 1) * 10;
    },
    to() {
      return this.from + this.perPage;
    },
    pageproducts() {
      return this.filteredProducts.slice(this.from, this.to);
    },
    total() {
      return this.products.length;
    },
    totalPages() {
      return Math.ceil(this.total / this.perPage);
    },
  },
  methods: {
    changePerPage(page) {
      this.perPage = page;
    },
    changeSortOrder(order) {
      this.sortOrder = order;
    },
    setSearchKey(searchKey) {
      this.searchKey = searchKey;
    },
    addProduct(productName) {
      if (productName) {
        const newProduct = {
          name: productName,
          date: new Date(),
          status: "green",
          image: "",
        };

        this.products.unshift(newProduct);
      }
    },
  },
};
</script>

<style scoped>
@import "./assets/css/styles.css";

.add-form-button {
  background-color: #377364;
  border-radius: 4px;
  padding: 11px 16px;
  color: #ffffff;
  font-size: 12px;
  line-height: 16px;
  font-family: "Inter", sans-serif;
  outline: none;
  appearance: none;
  border: 0;
  white-space: nowrap;
}

.products-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  column-gap: 30px;
}

@media (max-width: 600px) {
  .products-container {
    grid-template-columns: auto;
    column-gap: 30px;
  }
}
</style>
