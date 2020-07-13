<template>
        <div class="search">
            <input id="search"  name="search" :value="value" @input="handleChange" :class="{dark}">
        </div>
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
    .search{
        width:300px;
        display:flex;
        flex-direction: column;
        align-items: center;
    }
    input{
        height:30px;
        width:80%;
        border:0;
        color: white;
        border-bottom: 2px solid white;
        align-content: center;
        background: none;
        transition: box-shadow .3s ease-out;
    }
    input:focus{
        outline: none;
        box-shadow: -2px 24px 54px -13px white;
    }

    .dark{
        margin-top:150px;
        color: #111a38;
        border-bottom-color: #111a38;
    }
    .dark:focus{
        box-shadow: -2px 24px 54px -13px #111a38;
    }
</style>
