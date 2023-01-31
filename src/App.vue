<script setup>
import { h, ref } from "vue";
import HelloWorld from "./components/HelloWorld.vue";

const priceNow = ref(0);
</script>

<template>
  <div class="page">
    <div class="example">
      <img src="./assets/example.jpg" alt="" />
    </div>

    <div class="pricerow">
      <div class="now">
        <p>現在出價：{{ priceNow }}</p>
      </div>

      <div class="inputprice">
        <div class="inputtext">
          <p>Name：</p>
          <input type="text" />
        </div>
        <div class="inputtext">
          <p>Phone：</p>
          <input type="text" />
        </div>
        <div class="inputtext">
          <p>出價格：</p>
          <input type="text" />
        </div>
        <button>確定出價</button>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.page {
  display: flex;
  align-items: center;
  justify-content: center;
}
.example {
  width: 30%;
  img {
    width: 100%;
    border-radius: 15px;
  }
}
.inputprice {
  width: 20%;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: auto;

  .inputtext {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  button {
    width: 30%;
  }
}
</style>
