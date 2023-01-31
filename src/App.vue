<script setup>
import { h, ref } from "vue";
import HelloWorld from "./components/HelloWorld.vue";

const priceNow = ref(0);
</script>

<template>
  <div class="bar">
    <h1>FF40 | hidei掛軸拍賣 - 開拓動漫祭ww</h1>
  </div>

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
          <p>姓名：</p>
          <input type="text" />
        </div>
        <div class="inputtext">
          <p>電話號碼：</p>
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
.bar {
  border: 1px solid;
  width: 100vw;
  background-color: #ffffff;
  color: #101010;
  h1 {
    background-color: #ffffff;
  }
}
.page {
  display: flex;
  align-items: center;
}
.example {
  width: 50%;
  img {
    width: 100%;
    border-radius: 15px;
  }
}
.pricerow {
  display: flex;
  width: 50%;
  flex-direction: column;
  align-items: flex-start;
}
.inputprice {
  width: 50%;
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
    width: 100%;
  }
}
</style>
