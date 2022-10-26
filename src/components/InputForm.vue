<template>
  <form class="form" @submit.prevent="handleSubmit">
    <input v-model="dataInput" :placeholder="placeholder" class="form-input"/>
    <slot>
      <button type="submit" class="form-button">Search</button>
    </slot>
  </form>
</template>
<script>
export default {
  name: "inputForm",
  props: {
    placeholder: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      dataInput: null
    }
  },
  methods: {
    handleSubmit() {
      this.$emit('submit-data', this.dataInput)
    }
  }
};
</script>
<style scoped>
.form {
  display: flex;
  column-gap: 8px;
  width: 100%;
  justify-content: space-between;
  margin-bottom: 8px;
}

.form .form-input {
  border: 1px solid #e0e2e4;
  border-radius: 8px;
  background-color: #ffffff;
  padding: 8px 12px;
  font-size: 14px;
  line-height: 22px;
  font-weight: 400;
  color: #939597;
  font-family: "Inter", sans-serif;
  width: 100%;
}

.form .form-button {
  background-color: #375673;
  border-radius: 4px;
  padding: 11px 16px;
  color: #ffffff;
  font-size: 12px;
  line-height: 16px;
  font-family: "Inter", sans-serif;
  outline: none;
  appearance: none;
  border: 0;
}
</style>
