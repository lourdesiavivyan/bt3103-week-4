<template>
  <div>
    <h1>
      <button id = 'button2' v-on:click="decrease"> - </button>
      {{counter}}
      <button id='button1' v-on:click="increase"> + </button>
    </h1>
  </div>
</template>

<script>
export default {
  name: 'QuantityCounter',
  data () {
    return {
      counter : 0
    }
  },
  methods : {
    increase : function() {
      if (this.counter >= 10) {
        alert("You cannot buy more than 10 items.");
      } else {
        this.counter++;
      }
      this.$emit('counter', this.item, this.counter)
    },
    decrease : function() {
      if (this.counter > 0) {
        this.counter--;
      }
      this.$emit('counter', this.item, this.counter)
    }
  }, 
  props : {
    item : {
      type : Object
    }
  }
}
</script>


<style scoped>
  #button1, #button2 {
    background-color: pink; 
    border: 10px;
    color: black;
    text-align: center;
    font-size: 30px;
    display:inline-block;
  }
</style>
