<template>
    <input 
        id="search" 
        name="search"
        :class="{ dark }"
        :value="value"
        @input="handleChange"
    />
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
            type: String,
            required: true,
        },
    },
    methods: {
        handleChange(e) {
            this.$emit('input', e.target.value);
        }
    }
};
</script>

<style lang="scss" scoped>

    input {
        margin-top: 5vh;
        text-align: center;
        font-size: 18px;
        font-weight: 300;
        height: 30px;
        border: 0;
        border-bottom: 1px solid white;
        background: none;
        color: white;
        transition: box-shadow .5s;

        @media (min-width: 1024px) {
            font-weight: 400;
        }
    }

    input:focus {
        outline: none;
        box-shadow: 0 10px 20px -8px rgba(255, 255, 255, .6)
    }

    .dark {
        color: #1E3D4A;
        border-bottom-color: #1E3D4A;
    }

    .dark:focus {
        box-shadow: 0 10px 20px -8px rgba(#1E3D4A, .2);
    }

</style>