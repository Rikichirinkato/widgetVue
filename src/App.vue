<template>
  <article class="app">
    <div class="head" htmlFor="open">
      <h1 id="h1">Expenses</h1>
      <button class="open-btn" v-on:click="isOpen = !isOpen">
        <div id="left"></div>
        <div id="right"></div>
      </button>
    </div>
    <div class="info" v-bind:class="{ open: isOpen }">
      <div class="info-headers">
        <p>
          <span>Name</span>
          <button type="button" v-on:click="sortStuff()">↓</button>
        </p>
        <p>Amount</p>
    </div>
    <div class="list">
      <div class="cost" v-for="item in allStuff"><span>{{ item.stuff }}</span><span>{{ item.price }}</span></div>
    </div>
    <form>
      <input type="text" v-model="stuff" placeholder="Name"/>
      <input type="number" v-model="price" placeholder="$$.¢¢"/>
      <button type="button" v-on:click="addStuff()">+</button>
    </form>
  </div>
  <div class="total">
    <span>Total</span><span id="result"></span>
  </div>
  <HelloWorld :msg="'message'"/>
  </article>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
export default {
  components: {
    HelloWorld,
  },
  data: function() {
    return {
      allStuff: [],
      allAmounts: Array,
      isOpen: false,
      stuff: '',
      price: Number,
    }
  },
  methods: {
      addStuff() {
          this.allStuff.push({stuff: this.stuff, price: this.price});
          this.stuff = '';
          this.price = '';
      },

      sortStuff() {
        this.allStuff.sort((a, b) => a.stuff - b.stuff);
      }
  },
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
}
.app {
    max-width: 400px;
    height: auto;
    margin: auto;
    background-color: #edf1f9;
}
.head {
    width: inherit;
    height: 30px;
    border: 1px solid #3192af;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
}
h1 {
    color: #3192af;
}
.open-btn {
    width: 25px;
    height: 25px;
    border:1px solid #3192af;
    border-radius: 3px;
    margin-right: 3px;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
    background-color: inherit;
}
#left, #right {
    width: 2px;
    height: 20px;
    background-color: #3192af;
}
#left {
    transform: rotate(-30deg);
    margin-left: 3px;
}
#right{
    transform: rotate(30deg);
    margin-right: 3px;
}
#open:checked~.head .open-btn #left {
    transform: rotate(30deg);
}
#open:checked~.head .open-btn #right {
    transform: rotate(-30deg);
}
.info {
    width: inherit;
    height: 300px;
    border: 1px solid #3192af;
    border-top: 0;
    display: none;
}
.open {
  display: block;
}
.info-headers {
    width: 100%;
    height: 25px;
    display: flex;
    flex-direction: row;
}
.info-headers p {
    width: 50%;
    border-bottom: 1px solid #3192af;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
    background-color: #a7c3ef;
    height: 25px;
    box-sizing: border-box;
}
.list {
    width: inherit;
    height: 235px;
    overflow-y: auto;
}
.cost:nth-child(2n) {
    background-color: azure;
}
.cost {
    width: 100%;
    height: 25px;
    display: flex;
    flex-direction: row;
    align-items: center;
    border-bottom: 1px solid #3192af;
}
.cost span {
    width:48%;
    height: inherit;
    padding: 0 1%;
}
.cost span:last-child {
    border-left: 1px solid #3192af;
}
form {
    width: inherit;
    height: 40px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-around;
    border-top:  1px solid #3192af;
    background-color: #a7c3ef;
}
form input{
    width:40%;
    max-width: 165px;
    padding: 2px;
    border-radius: 3px;
    border: 1px solid #3192af;
}
button{
    width: 20px;
    height: 20px;
    border-radius: 3px;
    border: 1px solid #3192af;
    background-color: #3f87fc;
}
.total{
    width: inherit;
    height: 30px;
    border: 1px solid #3192af;
    display: none;
}
.total *{
    color: red;
}
.total span{
    width:48%;
    padding: 0 1%;
}
</style>
