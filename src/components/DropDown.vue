<template>
  <div class="drop-down" :tabindex="tabindex" @blur="open = false">
    <div class="selected" :class="{ open: open }" @click="open = !open">
      <h4>
        <b>{{ selected || placeholder }}</b>
      </h4>
      <img src="@/assets/icons/arrow-down.svg" alt="arrow-down" />
    </div>

    <div class="items" :class="{ selectHide: !open }">
      <div
        v-for="(option, index) in options"
        :key="index"
        @click="selectOption(option)"
        class="option-item"
      >
        <h4>
          {{ option }}
        </h4>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "DropDown",
  props: {
    options: {
      type: [Array, Number],
      default: () => [],
    },
    tabindex: {
      type: Number,
      default: 0,
    },
    default: {
      type: [String, Number],
      default: null,
    },
    placeholder: {
      type: String,
      default: null,
    },
  },
  data() {
    return {
      selected: this.default ? this.default : null,
      open: false,
    };
  },
  mounted() {
    this.$emit("input", this.selected);
  },
  methods: {
    selectOption(option) {
      this.selected = option;
      this.open = false;
      this.$emit("input", option);
    },
  },
};
</script>
<style scoped>
.drop-down {
  position: relative;
  width: 100%;
  text-align: left;
  outline: none;
}

.drop-down h4 {
  font-size: 12px;
  line-height: 16px;
  font-weight: 400;
  color: #252526;
}

.drop-down .items {
  min-width: 40px;
  display: flex;
  flex-direction: column;
  background-color: white;
  border-radius: 2px;
  row-gap: 4px;
}

.drop-down .items.selectHide {
  display: none;
}

.drop-down .items .option-item {
  padding: 2px 6px;
  cursor: pointer;
}

.drop-down .items .option-item:hover{ 
  background-color: #E0E2E4;
}

.drop-down .selected {
  display: flex;
  align-items: center;
  column-gap: 11.34px;
  cursor: pointer;
}

</style>
