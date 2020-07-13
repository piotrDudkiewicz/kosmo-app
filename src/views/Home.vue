<template>
  <div :class="[{flexStart: step == 1 },'wrapperHome']">
        <transition name="slide">
            <img v-if="step===1" src="../assets/COSMOS.png" class="logo">
        </transition>
      <transition name="fade">
          <Background-image v-if="step === 0"></Background-image>
      </transition>
      <Claim v-if="step === 0"/>
      <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1" />
    <div class="resultBox" v-if="results && !loading && step === 1">
        <Item v-for="item in results" :key="item.data[0].nasa_id" :item="item"
              @click.native="handleModalOpen(item)"/>
    </div>
      <Modal v-if="modalOpen" :data="modalData" @closeModal="modalOpen = false"/>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '../components/Claim.vue';
import SearchInput from '../components/SearchInput.vue';
import BackgroundImage from '../components/BackgroundImage.vue';
import Item from '../components/Item.vue';
import Modal from '../components/Modal.vue';

const api = 'https://images-api.nasa.gov/search';

export default {
  name: 'Home',
  data() {
    return {
      searchValue: '',
      results: [],
      loading: false,
      step: 0,
      modalOpen: false,
      modalData: null,
    };
  },
  methods: {
    handleInput: debounce(function () {
      this.loading = true;
      axios.get(`${api}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        }).catch((error) => console.log(error));
    }, 1000),
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalData = item;
    },
  },
  components: {
    Claim,
    SearchInput,
    BackgroundImage,
    Item,
    Modal,
  },
};
</script>

<style lang="scss" scoped>
  .wrapperHome{
      display: flex;
      position: relative;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 30px;
      margin: 0;
      width: 100%;
      min-height: 100vh;

      &.flexStart{
          justify-content: flex-start;
      }
  }
  .resultBox{
      margin-top:30px;
      display: grid;
      grid-template-columns: 1fr;
      grid-gap: 30px;

      @media(min-width: 768px){
          grid-template-columns: 1fr 1fr;
      }

      @media(min-width: 1026px){
          grid-template-columns: 1fr 1fr 1fr;
      }

  }

  .logo{
      position: absolute;
      width:130px;
      top:30px;
  }

  .fade-enter-active, .fade-leave-active {
      transition: opacity .5s ease;
  }
  .fade-enter, .fade-leave-to {
      opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
      transition: margin-top .5s ease;
  }
  .slide-enter, .slide-leave-to {
      margin-top: -80px;
  }
</style>
