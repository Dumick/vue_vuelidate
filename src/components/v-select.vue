<template>
  <div class="select">
    <span
      class="select__button"
      @click="changeStatus()"
      :class="isShow ? 'active' : ''"
      >{{ title }}</span
    >
    <ul class="select__option" :class="isShow ? 'active' : ''">
      <li
        v-for="(option, key) in options"
        :id="key"
        :key="key"
        @click="addOption($event)"
        class="select__option-item"
      >
        {{ option }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "v-select",
  data() {
    return {
      isShow: false,
      option: []
    };
  },
  methods: {
    changeStatus() {
      this.isShow = !this.isShow;
    },
    addOption(e) {
      const li = document.querySelectorAll(".select__option-item");

      if (!this.isMulty) {
        li.forEach((item) => item.classList.remove("active"));

        e.target.classList.add("active");
        this.$emit("update:modelValue", e.target.id);
      } else {
        const elem = e.target.id

        if (!this.option.includes(elem)) {
          e.target.classList.add("active");
          this.option.push(elem)
        } else {
          e.target.classList.remove("active");

          this.option.splice(this.option.indexOf(elem), 1)
          console.log(this.option);
        }

        this.$emit("update:modelValue", this.option);
      }
    },
  },
  props: {
    options: Object,
    title: String,
    isMulty: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style lang="scss">
$animationDuration: 0.3s;

.select {
  width: 250px;
  height: 35px;
  color: #000;
  background-color: #fff;
  position: relative;
  z-index: 20;

  &__button {
    display: inline-block;
    margin-top: 8px;
    width: 250px;
    height: 35px;

    position: relative;
    cursor: pointer;

    &:before {
      transition: $animationDuration;
      content: "";
      position: absolute;
      top: 9px;
      right: 16px;
      height: 2px;
      width: 8px;
      background-color: #000;
      transform: rotate(45deg);
    }
    &:after {
      transition: $animationDuration;
      content: "";
      position: absolute;
      top: 9px;
      right: 12px;
      height: 2px;
      width: 8px;
      background-color: #000;
      transform: rotate(-45deg);
    }

    &.active {
      &:before {
        transition: $animationDuration;
        content: "";
        position: absolute;
        top: 9px;
        right: 16px;
        height: 2px;
        width: 8px;
        background-color: #000;
        transform: rotate(-45deg);
      }
      &:after {
        transition: $animationDuration;
        content: "";
        position: absolute;
        top: 9px;
        right: 12px;
        height: 2px;
        width: 8px;
        background-color: #000;
        transform: rotate(45deg);
      }
    }
  }

  &__option {
    visibility: hidden;

    &.active {
      visibility: visible;
    }
    &-item {
      position: absolute;
      top: 0;
      width: 100%;
      height: 100%;

      padding: 8px 15px;
      background-color: #fff;

      cursor: pointer;
      list-style: none;

      &:nth-child(1) {
        margin-top: 40px;
      }
      &:nth-child(2) {
        margin-top: 75px;
      }
      &:nth-child(3) {
        margin-top: 110px;
      }
      &:hover {
        background-color: #ccc;
      }

      &.active {
        background-color: #74a4ff;
      }
    }
  }
}
</style>