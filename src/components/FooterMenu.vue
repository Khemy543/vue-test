<template>
  <div class="pagination-wrapper">
    <h3 class="paginator-text">
      Page <b>{{ currentPage }}</b> of <b> {{ totalPages }}</b>
    </h3>

    <div class="sort">
      <h3 class="paginator-text">Sort by</h3>
      <DropDown
        :options="['Asc', 'Desc']"
        placeholder="Sort Order"
        @input="$emit('change-sort-order', $event)"
      />
    </div>

    <div class="page-count">
      <DropDown
        :options="totalPages"
        :default="1"
        @input="$emit('change-page', $event)"
      />
    </div>
  </div>
</template>
<script>
import DropDown from "./DropDown.vue";

export default {
  name: "FooterMenu",
  props: {
    currentPage: {
      type: Number,
      required: true,
    },
    totalPages: {
      type: Number,
      required: true,
    },
  },
  components: { DropDown },
};
</script>
<style scoped>
.pagination-wrapper {
  padding: 16px;
  font-family: "Inter", sans-serif;
  display: flex;
  justify-content: space-between;
}

.paginator-text {
  font-size: 12px;
  line-height: 16px;
  font-weight: 400;
  color: #252526;
}

.page-count {
  display: flex;
  column-gap: 11.34px;
}

.sort {
  display: flex;
}

.sort h3 {
  white-space: nowrap;
  margin-right: 4px;
}
</style>
