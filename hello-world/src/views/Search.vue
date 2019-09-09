<template>
  <div class="wrapper">
      <Claim />
      <SearchInput />
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim';
import SearchInput from '@/components/SearchInput';

const API = 'https://images-api.nasa.gov';

export default {
  name: 'Search',
  components: { Claim, SearchInput, },

  data() {
      return {
          searchValue: '',
          results: [],
      }
  },
  methods: {
      handleInput: debounce(function() {
        axios.get(API+'/search?q='+this.searchValue+'&media_type=image')
            .then((response) => {
                console.log(response);
                this.results = response.data.collection.items;
                console.table(this.results)
            })
            .catch((error) => {
                console.log(error);
            })
      }, 500),
  },
}
</script>
<style lang="scss" scoped>
    .wrapper {
        margin: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        margin: 0;
        padding: 30px;
        height: 100vh;
        width: 100%;
        justify-content: center;
        background-image: url('../assets/heroimage.jpg');
        background-repeat: no-repeat;
        background-size: cover;
        background-position: 80% 0%;
    }

</style>

