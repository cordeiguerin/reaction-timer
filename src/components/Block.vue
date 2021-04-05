<template>
  <div v-if="showBlock" class="block" @click="stopTimer">
    Click Me!
  </div>
</template>

<script>
export default {
    name: "Block",
    props: ['delay'],
    data() {
        return {
            showBlock: false,
            timer: null,
            reactionTimer: 0
        }
    },
    mounted() {
        setTimeout(() => {
            this.showBlock = true
            this.startTimer()
        },  this.delay)
    },
    methods: {
        startTimer() {
            this.timer = setInterval(() => {
                this.reactionTimer += 10
            }, 10)
        },
        stopTimer(){
            clearInterval(this.timer)
            this.$emit("end", this.reactionTimer)
        }
    }
}
</script>

<style>
    .block {
        background-color: #A54F1A;
        color: antiquewhite;
        width: 60vw;
        margin: 10% auto;
        padding: 15vh 0;
        border-radius: 5px;
        font-weight: bold;
        cursor: pointer;
    }
</style>