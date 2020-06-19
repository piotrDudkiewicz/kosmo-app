<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search:</label>
      <input id="search" v-model="searchValue" @input="handleInput" name="search">
    </div>
    <div class="resultBox">
      <div class="resultItem" v-for="item in results" :key="item.data[0].nasa_id">
        <p>{{item.data[0].title}}</p>
        <img :src="item.links[0].href"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';

const api = 'https://images-api.nasa.gov/search';

export default {
  name: 'Home',
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      axios.get(`${api}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
        });
    }, 1000),
  },
};
</script>

<style lang="scss" scoped>
  *{
    box-sizing: border-box;
  }
  .wrapper{
    display: flex;
    flex-direction: column;
    align-items: center;
    margin:0;
    padding:30px;
    width: 100%;
  }
  .search{
    width:300px;
    display:flex;
    flex-direction: column;
    align-items: center;
  }
  input{
    height:30px;
    border:0;
    border-bottom: 1px solid black;
    align-content: center;
  }
  label{
    font-family: "Monotype Corsiva",sans-serif;
  }
  .resultBox{
    display: flex;
    flex-direction: row;
    flex-wrap:wrap;
    justify-content: center;
    align-items:stretch;
  }
  .resultItem{
    clear:both;
    display: flex;
    flex-direction: column;
    align-items: center;
    width:300px;
  }
  .resultItem img{
    padding: 5%;
    height:200px;
    width:300px;
  }
</style>
