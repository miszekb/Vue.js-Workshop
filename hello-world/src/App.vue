<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">

    <transition>
      <img src="./assets/logo.svg" class="logo" v-if="step === 1">
    </transition>

    <transition name="fade">
      <HeroImage v-if="step === 0"/>
    </transition>

    <Claim v-if="step === 0" />
    <SearchInput 
      v-model="searchValue" 
      @input="handleInput" 
      :dark="step === 1"
    />
    <div class="results" v-if="results && !loading && step === 1">
        <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id"
          @click.native="handleModalOpen(item)"/>
    </div>
    <Modal v-if="modalOpen" :item="modalData" @closeModal="modalOpen = false"/>
  </div>
</template>

<script>
  import axios from 'axios';
  import debounce from 'lodash.debounce';
  import Claim from '@/components/Claim';
  import SearchInput from '@/components/SearchInput';
  import HeroImage from '@/components/HeroImage';
  import Item from '@/components/Item';
  import Modal from '@/components/Modal';

  const API = 'https://images-api.nasa.gov';

  export default {
    name: 'App',
    components: { Claim, SearchInput, HeroImage, Item, Modal },

    data() {
        return {
            modalData: null,
            modalOpen: false,
            searchValue: '',
            results: [],
            loading: false,
            step: 0,
        }
    },
    methods: {
        handleModalOpen(item) {
          this.modalOpen = true;
          this.modalData = item;
        },

        handleInput: debounce(function() {
          this.loading = true;
          axios.get(API+'/search?q='+this.searchValue+'&media_type=image')
              .then((response) => {
                  this.results = response.data.collection.items;
                  this.loading = false;
                  this.step = 1;
              })
              .catch((error) => {
                  console.log(error);
              })
        }, 500),
    },
  }

</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800');

  * {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  body {
    font-family: 'Montserrat', sans-serif;
    margin: 0;
    padding: 0;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s ease;
  }

  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
    transition: margin-top .3s ease;
  }

  .slide-enter, .slide-leave-to {
    margin-top: -50px;
  }

  .wrapper {
    position: relative;
    margin: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    height: 100vh;
    width: 100%;
    justify-content: center;

  &.flexStart {
    justify-content: flex-start;
  }
}

.logo {
  position: absolute;
  top: 30px;
}

.results {
  margin-top: 5vh;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 20px;

  @media (min-width: 768px) {
      grid-template-columns: 1fr 1fr 1fr;
  }
}

</style>