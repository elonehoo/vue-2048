<script setup>
import { toRefs, computed } from "vue";

let props = defineProps({
    board: {
      type: Object,
      required: true,
    },
    onrestart: {
      type: Function,
      required: true,
    },
})

let { board } = toRefs(props);

let show = computed(() => {
    return board.value.hasWon() || board.value.hasLost();
});

let contents = computed(() => {
    if (board.value.hasWon()) {
        return "Good Job!";
    } else if (board.value.hasLost()) {
        return "Game Over";
    } else {
        return "";
    }
});

let restart = () => {
      props.onrestart && props.onrestart();
}
</script>

<template>
  <div class="overlay" v-show="show">
    <p class="message">{{ contents }}</p>
    <button class="tryAgain" @click="restart">Try again</button>
  </div>  
</template>

<style>

</style>