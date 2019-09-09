<template>
  <div class="searchWrapper">
    <label for="search">Search</label>
        <input 
            id="search" 
            name="search"
            v-model="searchValue"
            @input="handleInput"
        />
  </div>
</template>

<script>
export default {
    name: 'SearchInput',
};
</script>

<style lang="scss" scoped>
    .searchWrapper {
        margin-top: 50px;
        display: flex;
        flex-direction: column;
        width: 250px;

        label {
            display:none;
            font-family: Montserrat, sans-serif
        }

        input {
            height: 30px;
            border: 0;
            border-bottom: 1px solid black;
            background: none;
        }
    }
</style>