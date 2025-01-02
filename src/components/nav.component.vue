<script lang="tsx" setup>
import logo from "./../assets/logo.png";
</script>

<style lang="scss">
header {
  nav {
    display: flex;
    justify-content: space-between;
    padding: 0.2rem 0.5rem;
    background-color: #dadde2;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  .left {
    img {
      width: 100px;
    }
  }
}
</style>

<template>
  <header>
    <nav>
      <div class="left">
        <img :src="logo" alt="logo-image" />
      </div>
    </nav>
  </header>
</template>
