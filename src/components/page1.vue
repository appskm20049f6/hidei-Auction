<script setup>
import { h, ref } from "vue";
import axios from "axios";

var config = {
  method: "get",
  maxBodyLength: Infinity,
  url: "https://script.google.com/macros/s/AKfycbx934MrKutaOtSAT9DtmUJp7NkES6cp0D0JfgGu995XwE7v34F6Q1hozGdyOKEAek-WuA/exec",
};
const hightlest = ref("目前最高價：");
let priceNow = ref("???");
let loading = ref(0);
let Today = new Date();
let name = ref("");
let phone = ref("");
let pricepush = ref();
let post = ref("");

axios(config)
  .then(function (res) {
    priceNow.value = parseInt(res.data[res.data.length - 1][1]);
    return priceNow.value;
  })
  .catch(function (error) {
    console.log(error);
  });

let checkPrice = () => {
  axios(config)
    .then(function (res) {
      priceNow.value = parseInt(res.data[res.data.length - 1][1]);
      return priceNow.value;
    })
    .catch(function (error) {
      console.log(error);
    });
};

// 30秒更新最高價
// setInterval(() => {
//   checkPrice();
// }, 30000);

let pricepushtop = (e) => {
  if (overLine.value <= 0) {
    alert("已經截止無法投標囉！");
  } else {
    if (pricepush.value >= priceNow.value + 100) {
      if (post.value == "626") {
        fetch("https://sheetdb.io/api/v1/zhq1olshj449h", {
          method: "POST",
          headers: {
            Accept: "application/json",
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            data: [
              {
                time: `${Today}`,
                pricepush: `${pricepush.value}`,
                name: `${name.value}`,
                phone: `${phone.value}`,
              },
            ],
          }),
        }).then((res) => {
          checkPrice();
          alert("競標出價成功!");
        });
      } else {
        alert("驗證碼輸入錯誤");
      }
    } else {
      alert("競標金額要高於最高價100喔！");
    }
  }
};

const endtime = new Date("2023-02-05 16:00");
let nowTime = new Date();

let overLine = ref((endtime - nowTime) / 1000);

let hr = ref(parseInt(overLine.value / 60 / 60));
let min = ref(parseInt((overLine.value / 60) % 60));
let secsec = ref(parseInt(overLine.value % 60));

const timer = setInterval(() => {
  secsec.value = secsec.value - 1;

  if (secsec.value == -1) {
    secsec.value = 59;
    min.value = min.value - 1;
    if (min.value == -1) {
      hr.value = hr.value - 1;
      if (hr.value < 0) {
        secsec.value = 0;
        min.value = 0;
        hr.value = 0;
        clearInterval(timer);
        location.reload();
      }
    }
  }
  overLine.value = overLine.value - 1;
}, 1000);

if (overLine.value <= 0) {
  secsec.value = 0;
  min.value = 0;
  hr.value = 0;
  hightlest.value = "得標價：";
  alert("競標已經截止囉！");
  clearInterval(timer);
}
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
      <img src="../assets/example3.jpg" alt="" />
    </div>

    <div class="pricerow">
      <h1>逸仙(裸圍ver.)75*105大掛軸</h1>
      <hr />
      <p>唯一一支，絕無再版！喜歡的話歡迎動動小指頭出價把它帶回家٩(˃̶͈̀௰˂̶͈́)و</p>
      <p>結標時間到會立刻打電話給得標者喔！姓名請打真實姓名（可以備註暱稱）</p>
      <p>⚠️驗證碼請直接問拜寧 以防止有人惡意搗蛋亂標⚠️</p>
      <div class="price">
        <div class="priceup">
          <p>起價：</p>
          <p>TWD：500</p>
        </div>
        <div class="pricenow">
          <p>{{ hightlest }}</p>
          <p>TWD：{{ priceNow }}</p>
        </div>
      </div>
      <div class="timeout">
        <p>結束尚餘：{{ hr }}時{{ min }}分鐘{{ secsec }}秒</p>
      </div>
      <div class="inputprice">
        <div class="inputtext">
          <p>真實姓名：</p>
          <input v-model="name" type="text" placeholder="暱稱可" />
        </div>
        <div class="inputtext">
          <p>電話號碼：</p>
          <input v-model="phone" type="text" placeholder="不填怎麼聯絡！" />
        </div>
        <div class="inputtext">
          <p>競標出價：</p>
          <input
            v-model="pricepush"
            type="text"
            placeholder="每次競標最少+100!"
          />
        </div>
        <div class="inputtext">
          <p>驗證碼：</p>
          <input type="text" v-model="post" placeholder="驗證碼問拜寧" />
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
      font-size: larger;
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
      width: 30%;
      justify-content: flex-start;
      @media screen and (max-width: 900px) {
        width: 45%;
      }
      @media screen and (max-width: 414px) {
        width: 35%;
      }
      @media screen and (max-width: 360px) {
        width: 48%;
      }
    }
    input {
      width: 40%;
    }
  }
}
</style>
