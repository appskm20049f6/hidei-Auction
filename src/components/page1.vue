<script setup>
import { h, ref } from "vue";
import axios from "axios";
const priceNow = ref(500);
const sen = ref(30);
const sec = ref(59);

let Today = new Date();
let name = ref("");
let phone = ref("");
let pricepush = ref(0);

let post = ref("");

console.log(Today);

const datadata = {
  time: Today,
  name: name.value,
  phone: phone.value,
  pricepush: pricepush.value,
};

var config = {
  method: "post",
  url: "https://sheetdb.io/api/v1/zhq1olshj449h",
  data: datadata,
};

let pricepushtop = (e) => {
  if (pricepush.value > priceNow.value) {
    if (post == "0205") {
      axios(config)
        .then(function (res) {
          console.log(res);
        })
        .catch(function (error) {
          console.log(error);
        });
    } else {
      alert("驗證碼輸入錯誤");
    }
  } else {
    alert("競標金額低於現在金額哦～");
  }
};
</script>

<template>
  <div class="bar">
    <div><h1>FF40 | heidi掛軸拍賣</h1></div>
  </div>
  <div class="nav">
    <h2><a href="javascript:alert('目前還沒有喔<3');"> ↩單人掛軸</a></h2>
    <h2><a href="javascript:alert('目前還沒有喔<3');"> 雙人掛軸↪</a></h2>
  </div>
  <div class="page">
    <div class="example">
      <img src="../assets/example2.jpg" alt="" />
    </div>

    <div class="pricerow">
      <h1>單人掛軸</h1>
      <p>
        日本展場限量 來場者限定 B1 掛軸 全新 未拆 日本空運直送抵台現貨
        僅此一張~~ 下單前請先詢問，逕自下單者 賣家將只寄賣場圖片
      </p>
      <div class="price">
        <div class="priceup">
          <p>起價</p>
          <p>TWD：500</p>
        </div>
        <div class="pricenow">
          <p>目前最高價：</p>
          <p>TWD：{{ priceNow }}</p>
        </div>
      </div>
      <div class="timeout">
        <p>結束尚餘：{{ sen }}分鐘{{ sec }}秒</p>
      </div>
      <div class="inputprice">
        <div class="inputtext">
          <p>真實姓名：</p>
          <input v-model="name" type="text" />
        </div>
        <div class="inputtext">
          <p>電話號碼：</p>
          <input v-model="phone" type="text" />
        </div>
        <div class="inputtext">
          <p>競標出價：</p>
          <input v-model="pricepush" type="text" />
        </div>
        <div class="inputtext">
          <p>驗證碼：</p>
          <input
            type="text"
            v-model="post"
            placeholder="今天的日期是？A:0205"
          />
        </div>
      </div>
      <button @click="pricepushtop()">輸入資料參與競標</button>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.bar {
  padding: 1.5%;
  display: flex;
  width: 100vw;
  height: 10%;
  background-color: #ffffff;
  color: #101010;
  align-items: center;
  h1 {
    background-color: #ffffff;
    @media screen and (max-width: 414px) {
      font-size: 1.6rem;
    }
  }
}
.nav {
  display: flex;
  width: 100vw;
  color: #101010;
  justify-content: space-between;
  border: 1px solid #dfe1e1;
  h2 {
    margin: 1%;
    margin-left: 2%;
    margin-right: 2%;
    color: rgba(86, 63, 46, 1);
    a {
      color: rgba(86, 63, 46, 1);
    }
  }
}
.page {
  margin: auto;
  width: 90%;
  display: flex;
  align-items: center;
  justify-content: center;
  @media screen and (max-width: 900px) {
    flex-direction: column;
  }
  @media screen and (max-width: 414px) {
    width: 90%;
  }
}
.example {
  padding: 1%;
  display: flex;
  width: 40%;
  align-items: center;
  justify-content: center;
  @media screen and (max-width: 900px) {
    width: 65%;
  }
  @media screen and (max-width: 414px) {
    width: 90%;
  }
  img {
    padding: 1%;
    width: 98%;
    height: 98%;
    border-radius: 15px;
    background-color: #ffffff;
  }
}
.pricerow {
  padding: 1%;
  display: flex;
  width: 50%;
  flex-direction: column;
  align-items: flex-start;
  border-bottom: 1px solid #dfe1e1;
  @media screen and (max-width: 414px) {
    width: 90%;
  }
  button {
    margin-top: 2%;
    width: 100%;
    color: white;
    background-color: #563f2e;
  }
  h1 {
    @media screen and (max-width: 414px) {
      font-size: xx-large;
    }
  }
}
.price {
  margin-top: 3%;
  margin-bottom: 3%;
  width: 100%;
  display: flex;
  .priceup {
    width: 30%;
    font-size: 1.3rem;
    border-right: 1px solid #dfe1e1;
    @media screen and (max-width: 414px) {
      width: 40%;
    }
  }
  .pricenow {
    margin-left: 5%;
    font-size: 1.3rem;
  }
}
.inputprice {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  margin: auto;
  @media screen and (max-width: 900px) {
    margin-top: 4%;
  }

  .inputtext {
    width: 60%;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    @media screen and (max-width: 900px) {
      margin-top: 1%;
      width: 100%;
      justify-content: center;
    }
    p {
      display: flex;
      width: 40%;
      justify-content: flex-start;
      @media screen and (max-width: 900px) {
      }
    }
    input {
      flex-grow: 1;
    }
  }
}
</style>
