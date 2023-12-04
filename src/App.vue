<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <p>Was machst du hier????</p>
  <div>
    <pre>
      ________________________________________________
      |      _____________________________           |
      | [][] _____________________________ [_][_][_] |
      | [][] [_][_][_] [_][_][_][_] [_][_] [_][_][_] |   ____            _   _ 
      |                                              |  |  _ \          | | (_)
      | [][] [][][][][][][][][][][][][][_] [][][][]  |  | |_) | __ _ ___| |_ _ 
      | [][] [_][][][][][][][][][][][][][] [][][][]  |  |  _ &lt; / _` / __| __| |
      | [][] [__][][][][][][][][][][][][_] [][][][]  |  | |_) | (_| \__ \ |_| |
      | [][] [___][][][][][][][][][][][__] [__][][]  |  |____/ \__,_|___/\__|_|
      |          [_][______________][_]              |
      |______________________________________________|
    </pre>
    <p>
      <span>Welcome to my web terminal.</span>
    </p>
    <p class="text">
      <span>To list all commands, type </span>
      <span class="highlight">help</span>
      <span>.</span>
    </p>
  </div>
  <RouterView />
</template>

<style scoped>
pre {
  color: #4E9A06;
}
p {
  color: burlywood;
  white-space: nowrap;
}
.text {
  display: block;
  line-height: 1.3em;
  margin: 0;
}
</style>
