<template>
        <div :style="style" class="item" />
</template>

<script>
export default {
  name: 'Item',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: null,
      title: null,
    };
  },
  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
  },
  computed: {
    style() {
      return `background-image: url("${this.photo}");`;
    },
  },
};
</script>

<style lang="scss" scoped>
        .item{
            width:70vw;
            height:250px;
            background-size: cover;
            background-repeat: no-repeat;
            background-position: 50%;
                @media (min-width: 768px){
                        width:40vw;
                }
                @media (min-width: 1024px){
                        width:20vw;
                }
        }
</style>
