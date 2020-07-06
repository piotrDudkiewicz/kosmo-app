<template>
    <div class="wrapperImage"></div>
</template>

<script>
export default {
  name: 'BackgroundImage',
};
</script>

<style scoped>
.wrapperImage{
    width: 100%;
    height: 100vh;
    position: fixed;
    z-index: -1;
    top:0;
    background-image: url("../assets/background.jpg");
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-position: 70% 45%;
}
</style>
