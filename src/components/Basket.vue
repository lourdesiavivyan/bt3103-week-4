<template>
  <div>
    <h1> Welcome to the Restaurant </h1>
    <h1>Menu: </h1>
    <ul>
      <li v-for="(item,index) in itemsSelected" :key="index" >
        <h2>
            {{item[0]}} x {{item[1]}}
        </h2>
      </li>
    </ul>
    <button id="calculate" v-on:click="findTotal()"> Calculate Total </button>
    <h2 v-show = "showTot"> Subtotal : ${{subTotal}} </h2>
    <h2 v-show = "showTot"> Grandtotal : ${{grandTotal}} </h2>
  </div>
</template>

<script>
export default {
    data() {
      return {
        subTotal : 0, 
        grandTotal : 0,
        showTot : false
      }
    },
    props: {
      itemsSelected: {
        type: Array
      }
    }, 
    methods: {
      findTotal : function() {
        var total = 0;
        for (let i = 0; i < this.itemsSelected.length; i++) {
          total += (this.itemsSelected[i][1] * this.itemsSelected[i][2]);
        }
        this.subTotal = total.toFixed(2); 
        this.showTot = true;
      }
    },
    watch : {
      subTotal() {
        this.grandTotal = (this.subTotal * 1.07).toFixed(2);
      }
    }
  }
</script>


<style scoped>
 #calculate {
    background-color: pink; 
    border: 10px;
    color: black;
    text-align: center;
    font-size: 15px;
    display:inline-block;
  }
</style>
