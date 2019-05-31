<template>
  <!-- <v-layout column justify-center align-center > -->
  <v-layout>
    <!-- <v-flex xs12 sm8 md6> -->
    <v-flex>
      <!-- <div class="text-xs-right"> -->
        <no-ssr>
          <vue-typer text="민 인터랙트"
            :repeat='Infinity'
            :shuffle='true'
            initial-action='typing'
            :pre-type-delay='70'
            :type-delay='150'
            :pre-erase-delay='2000'
            :erase-delay='250'
            erase-style='backspace'
            :erase-on-complete='true'
            caret-animation='expand'
          ></vue-typer>
        </no-ssr>
      <!-- </div> -->
    </v-flex>
  </v-layout>

  <!-- <div>
    <vue-particles color="#dedede"></vue-particles>
  </div> -->
</template>

<script>
if (process.browser) {
  var VueTyper = require('vue-typer').VueTyper
}

export default {
  components: {
    VueTyper
  }
}
</script>

<style >
.vue-typer {
  font-family: Copperplate, 'Copperplate Gothic Light', fantasy;
}

.vue-typer .custom.char.typed {
  color: white;
  font-size: 4.5em;
}
.vue-typer .custom.char.selected {
  color: white;
  /* font-size: 8em; */
  background-color: transparent;
  /* text-decoration: line-through; */
}

.vue-typer .custom.caret {
  /* display: none; */
  color: yellow;
}
</style>
