<template>
  <div class="claimWrapper">
    <h1 class="claim">SPACER</h1>
    <p class="subclaim">
        Begin your journey through our amazing galaxy
        and discover places you never heard of.
    </p>
    <p class="subclaim">
        Type anything space-related to start.
    </p>
  </div>
</template>

<script>
export default {
    name: 'Claim',
}
</script>

<style lang="scss" scoped>
    .claimWrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        font-family: Montserrat, sans-serif;
        color: white;
    } 

    .claim {
        font-size: 50px;
        margin: 0;

        @media (min-width: 768px) {
            font-size: 80px;
        }
    }

    .subclaim {
         margin: 20px 0 0 0;
         font-size: 13px;

         @media (min-width: 768px) {
            font-size: 25px;
            letter-spacing: 1px;
            width: 500px;
            font-weight: 300;
        }
    }

</style>