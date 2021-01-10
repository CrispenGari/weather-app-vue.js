<template>
  <div class="header">
    <div class="header__nav__iterm">Home</div>
    <div class="header__nav__iterm">Weather &#x1F326;;</div>
  </div>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: sticky;
  top: 0;
  z-index: 10;
  padding: 10px;
}
.header__nav__iterm {
  color: white;
  text-decoration: none !important;
  font-weight: 500;
  letter-spacing: 2px;
  cursor: pointer;
  user-select: none;
  font-size: 17px;
  transition: transform 100ms ease-in-out linear;
}
.header__nav__iterm:hover {
  transform: scale(1.09);
}
</style>
