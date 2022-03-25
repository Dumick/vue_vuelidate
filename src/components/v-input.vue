<template>
  <div class="custom__input">
    <input
      :name="id"
      :type="inputType"
      :value="modelValue"
      @focus="focusInput"
      @input="$emit('update:modelValue', $event.target.value)"
    />
    <span :class="id" :name="id" @click="focusInput">{{ text }}</span>
    <span v-if="this.error">{{ error }}</span>
  </div>
</template>

<script>
export default {
  name: "v-input",
  props: {
    id: String,
    text: String,
    error: String,
    modelValue: String,
    inputType: {
      type: String,
      default: "text",
    },
  },
  methods: {
    focusInput() {
      document.querySelector("." + this.id).classList.add("active");
      document.querySelector('input[name="' + this.id + '"]').focus();
    },
  },
  watch: {
    error: () => {
      if (this.error) document.getElementById(this.id).classList.add("error");
      else document.getElementById(this.id).classList.remove("error");
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,400;0,500;1,400&family=Rubik&display=swap");

.custom__input {
  display: inline-block;
  width: 250px;
  border: none;
  background-color: #284ffd;
  position: relative;

  input {
    font-family: "Roboto", sans-serif;
    font-size: 16px;

    width: 100%;
    height: 35px;
    outline: none;
    padding: 8px 20px;
    transition: 0.2s;
    border: none;
    border-bottom: 2px solid #ffffff;

    &.error {
      border-bottom: 2px solid #fd5a28;
    }
  }

  span {
    position: absolute;
    top: 7px;
    left: 20px;
    font-size: 18px;
    color: black;
    transition: 0.2s;
    background-color: #fff;

    &.active {
      top: -20px;
      left: 10px;
      font-size: 14px;
      color: #fff;
      background-color: transparent;
    }

    &.error {
      color: #fd5a28;
    }
  }
}
</style>