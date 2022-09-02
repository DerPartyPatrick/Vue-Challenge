<script setup>
  import { ref } from 'vue'

  const current = ref(0)
  const animate = ref(true)
  const vocab = ref([
    {
      german: "Person", 
      korean: "사람", 
      views: 0
    }, 
    {
      german: "essen", 
      korean: "먹다", 
      views: 0
    }, 
    {
      german: "gehen", 
      korean: "가다", 
      views: 0
    }, 
    {
      german: "lernen",
      korean: "배우다", 
      views: 0
    }, 
    {
      german: "Krankenhaus", 
      korean: "병원", 
      views: 0
    }, 
    {
      german: "Freund", 
      korean: "친구", 
      views: 0
    }
  ])

  function toggleTranslation(index) {
    animate.value = false; 
    if(current.value == index) {
      current.value = -1; 
    }
    else {
      vocab.value[index].views++
      current.value = index; 
    }

    setTimeout(() => {
      animate.value = true
    }, 0.4)
  }
</script>

<template>
  <main>
    <h1>Koreanische Vokabeln</h1>
    <p>한국어 단어들</p>

    <br><br>
    <div v-for="(word, index) in vocab">
      <div @click="toggleTranslation(index)">
        <h3 v-if="current == index" style="color:white; cursor: pointer;">  {{ index+1 }}. {{ word.german }}</h3>
        <h3 v-else style="cursor: pointer;">{{ index+1 }}. {{ word.german }}</h3>
      </div>
    </div> 
    
    <br><br>
    <div class="move" v-if="current < 0">
      <p>Please select a word to view its translation.</p>
    </div>
    <div :class="{ move: animate }" v-else>
      <h3>{{ vocab[current].german }}</h3>
      <h3>{{ vocab[current].korean }}</h3>
      <p>views: {{ vocab[current].views }}</p>
    </div>


  </main>
</template>

<style scoped>
.move {
    animation: move; 
    animation-duration: 0.4s; 
  }

  @keyframes move {
    0% {transform: translate3d(-100px, 0, 0);} 
    100% {transform: translate3d(0, 0, 0);}
  }

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
