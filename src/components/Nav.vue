<template>
  <div class="nav">
    <div class="logo">
      <div class="toggleAside" @click.stop="toggleMenu" v-if="toggleMenuButtonVisible">
        <Icon name="menu"></Icon>
      </div>
      <router-link to="/">
        <img class="nav-logo" src="../assets/WheelHub-Plus.svg" alt="WheelHub-Plus">
      </router-link>
    </div>
    <ul class="menu">
      <li>
        <router-link to="/doc/intro">文档</router-link>
      </li>
      <li>
        <a href="https://github.com/Leslie-LiangGangwei/WheelHub-Plus">GitHub</a>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import {inject, ref} from "vue";
import Icon from "../lib/Icon.vue"

export default {
  name: "Nav",
  components: {Icon},
  props: {
    toggleMenuButtonVisible: {
      type: Boolean,
      default: false
    }
  },
  setup() {
    const menuVisible = inject<ref<boolean>>('menuVisible') // get
    const bgVisible = inject<ref<boolean>>('bgVisible')
    const toggleMenu = () => {
      menuVisible.value = !menuVisible.value
      bgVisible.value = !bgVisible.value
    }
    return {toggleMenu}
  }
}
</script>

<style scoped lang="scss">
$black-color: #252525;
$blue: #2973f5;

.nav {
  z-index: 20;
  position: fixed; top: 0; left: 0;
  width: 100%;
  display: flex; justify-content: center; align-items: center;
  padding: 24px;
  height: 64px;
  .logo {
    margin-right: auto;
  }
  .toggleAside {
    position: absolute;
    left: 16px;
    top: 50%;
    transform: translateY(-50%);
    display: none;
    .g-icon {
      width: 20px;
      height: 20px;
    }
  }
  .nav-logo {
    max-width: 9em;
    margin-right: auto;
  }
  .menu {
    display: flex;
    white-space: nowrap; flex-wrap: nowrap;
    li {
      display: flex;
      justify-content: center; align-items: center;
      color: $black-color;
      font-size: 16px;
      height: 32px;
      margin: 0 1em;
      a {
        color: $black-color;
        text-decoration: none;
        &:hover {
          color: $blue;
        }
      }
    }
  }
  @media (max-width: 576px) {
    .menu {
      display: none;
    }
    .logo {
      margin: 0 auto;
    }
    .toggleAside {
      display: inline-block;
    }
  }
}
</style>