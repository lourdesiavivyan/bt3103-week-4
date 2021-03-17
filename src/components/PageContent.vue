<template>
  <div>
      <ul id = "itemsList">
        <li v-for="item in itemsList" v-bind:key="item.name" >
            <p id = "itemName">{{item.name}}</p>
            <img v-bind:src="item.imageURL"/>   
            <br> 
            <p id = "price"> ${{item.price}}</p>
            <QuantityCounter v-bind:item="item" v-on:counter="onCounter"> </QuantityCounter>   
        </li>
        </ul>
        <Basket id="shoppingBasket" v-bind:itemsSelected="itemsSelected"> </Basket>
  </div>
</template>

<script>
import QuantityCounter from './QuantityCounter.vue'
import Basket from './Basket.vue'

export default {
  name: 'PageContent',
  data () {
    return {
      itemsSelected : [],
      itemsList: [
        {
          id: "#000",
          name: "Prawn omelette",
          imageURL:
            "https://3.bp.blogspot.com/-SMxoySoXcK0/T696enjIijI/AAAAAAAACoc/A5bFWd024KY/s1600/IMG_5140.JPG",
          price: 5,
        },
        {
          id: "#025",
          name: "Dry Beef Hor Fun",
          imageURL:
            "https://delishar.com/wp-content/uploads/2016/04/Dry-Beef-Hor-Fun-3.jpg",
          price: 15,
          
        },
        {
          id: "#067",
          name: "Sambal KangKung",
          imageURL:
            "https://minikitchenlab.com/wp-content/uploads/2017/09/Kangkung-Belacan-e1506580822679-1300x1300.jpg",
          price: 10,
        },
        {
          id: "#077",
          name: "Pork Fried Rice",
          imageURL:
            "https://hazeldiary.com/wp-content/uploads/2020/08/King-of-Fried-Rice-Golden-Mile-Tower-XO-Fried-Rice.jpg",
          price: 6,
        },
        {
          id: "#099",
          name: "Mapo Tofu",
          imageURL:
            "https://i2.wp.com/seonkyounglongest.com/wp-content/uploads/2020/09/Mapo-Tofu-12-minijpg.jpg?fit=1000%2C1500&ssl=1",
          price: 10,
        },
        {
          id: "#200",
          name: "Cereal Prawn",
          imageURL:
            "https://i.pinimg.com/originals/ad/87/eb/ad87eb2113e4d6480a21acdbb5f36114.jpg",
          price: 12,
        },
      ]
    }
  },
  components : {
    QuantityCounter,
    Basket
  }, 
  methods : {
    onCounter: function (item, count) {
      var doneAction = false; 
      if (this.itemsSelected.length === 0 && count > 0) {
        //If there is nothing in items selected, push the ORDER in
        this.itemsSelected.push([item.name, count, item.price]);
        doneAction = true;
      } else {
        // Loop through everything to check what is not in the basket
        for (let i = 0; i < this.itemsSelected.length; i++) {
          const curr_item = this.itemsSelected[i];
          const item_name = curr_item[0];

          // if item_name is the same as item.name and the count is more than 0, update this.itemsSelected
          if (item_name===item.name && count > 0) {
            this.itemsSelected.splice(i,1);
            this.itemsSelected.push([item.name, count, item.price]);
            doneAction = true;
            break;
          }
          // Next, item_name is the same as item.name and the count is 0, remove it from itemsSelected.
          else if (item_name===item.name && count === 0) {
            this.itemsSelected.splice(i,1);
            doneAction = true;
            break;
          }
        }
        // otherwise, if the item is not in itemSelected, add it to itemsSelected by pushing the ORDER in.
        if (!(doneAction) && count != 0) {
            this.itemsSelected.push([item.name, count, item.price]);
        }
      }
    },
  }
}
</script>

<style scoped>
  #itemsList {
    width: 100%;
    max-width: 70%;
    margin: 0px;
    padding: 0 5px;
    box-sizing: border-box;
  }
  ul {
    display: flex;
    flex-wrap: wrap;
    list-style-type: none;
    padding: 0;
  }
  li {
    flex-grow: 1;
    flex-basis: 300px;
    text-align: center;
    padding: 10px;
    border: 1px solid #222;
    margin: 10px;
  }
  img {
    width: 135px;
    height: 135px;
  }

  #price {
    font-size: 30px;
  }

  #itemName {
    font-size: 30px;
  }

  #shoppingBasket {
    position: absolute;
    top: 23%;
    left: 78%;
  }
</style>