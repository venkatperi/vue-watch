<template>
  <div>
    <vue-watch :dispatch="{text: 'textChanged'}">
      <text-component />
    </vue-watch>
    <div class="info" v-html="theEvent"></div>
  </div>
</template>


<script>
  import Vue from 'vue'
  import VueWatch from '../../../src'

  const TextComponent = Vue.component('text-component', {
    data() {
      return {
        text: '',
      }
    },
    template: '<textarea v-model="text" class="input2"></textarea>',
  } )

  export default {

    components: {
      VueWatch, TextComponent,
    },

    data() {
      return {
        theEvent: '',
      }
    },

    mounted() {
      const that = this
      this.$el.addEventListener( 'textChanged', function ( e ) {
        that.theEvent = e.detail
      } )
    },
  }
</script>

<style lang="scss">
  #app {
    margin-left: auto;
    margin-right: auto;
    width: 50%;
    text-align: center;
  }

  label, .info {
    font-size: 12px;
    font-family: sans-serif;
    width: 100%;
  }

  .input2 {
    width: 100%;
    margin-top: 10px;
    resize: none;
    background: #eee;
    border: #aaa solid 1px;
    border-radius: 3px;
    font-size: 20px;
  }


</style>

