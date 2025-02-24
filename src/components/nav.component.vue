<script lang="tsx" setup>
import logo from "./../assets/logo.png";
</script>

<style lang="scss">
header {
  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.2rem 0.5rem;
    background-color: #dadde2;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  .left {
    img {
      width: 100px;
    }
  }
  .right {
    a {
      text-decoration: none;
      padding: 10px 20px;
      color: #000;
      background-color: #ffa500;
      /* margin-right: 15px; */
      border-radius: 5px;
      &:hover {
        background-color: #ffbb3b;
      }
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
      <div class="right">
        <a
          href="https://medium.com/@sbrakeshrath/database-less-otp-a-concept-b73100fec797"
          >Blog</a
        >
      </div>
    </nav>
  </header>
</template>
