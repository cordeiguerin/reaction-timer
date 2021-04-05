<template>
  <p>Reaction Time: {{score}}ms</p>
  <h2>{{this.rank}}</h2>
</template>

<script>
export default {
    props: ['score'],
    data() {
        return {
            rank: null
        }
    },
    mounted() {
        if (this.score < 250) {
            this.rank = 'Ninja Fingers!'
        } else if (this.score < 400) {
            this.rank = 'Rapid Reflexes!'
        } else {
            this.rank = 'Snail Pace...'
        }
    }
}
</script>

<style>

</style>