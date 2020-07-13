<template>
<div class="outerWrapper">
    <div class="innerWrapper">
            <img :src="photo" alt="title">
        <div class="information">
            <h2 class="title">{{ title }}</h2>
            <p class="description">
                {{ description }}
            </p>
        </div>
    </div>
    <div class="close" @click="$emit('closeModal')"/>
</div>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    data: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: null,
      title: null,
      description: null,
    };
  },
  mounted() {
    this.photo = this.data.links[0].href;
    this.title = this.data.data[0].title;
    this.description = this.data.data[0].description.substr(0, 200);
  },
};
</script>

<style lang="scss" scoped>
    .outerWrapper{
        max-width: 100%;
        height: 100%;
        position: fixed;
        top:0;
        left: 0;
        padding: 30px;
        background: #f6f6f6;
        color:black;

        @media (min-width: 1024px){
            max-width: 80%;
            height: 70%;
            left:0;
            right:0;
            top:0;
            bottom: 0;
            margin:auto;
            box-shadow: 0 30px 30px -10px rgba(0,0,0,0.3);
        }
    }

    .innerWrapper{
        display: flex;
        height: 100%;
        padding: 50px;
        justify-content: center;
        align-items: center;
        flex-direction: column;

        img{
            width:100%;
        }

        @media (min-width: 1024px){
            flex-direction: row;

            img{
                padding: auto;
                padding-right:30px;
                max-height: 100%;
                object-fit: contain;
            }
        }

        @media (orientation: landscape){
            flex-direction: row;

            img{
                padding: auto;
                padding-right:30px;
                max-height: 100%;
                object-fit: contain;
            }
        }
    }

    .close{
        position: absolute;
        width: 30px;
        height: 30px;
        padding: 25px;
        right: 0;
        top:0;

        &::before,
        &::after{
            content: '';
            width: 30px;
            height:2px;
            position: absolute;
            right: 20px;
            top:20px;
            background: black;
            display: block;
        }

        &::before{
            transform: rotate(45deg);
        }

        &::after{
            transform: rotate(-45deg);
        }
    }
</style>
