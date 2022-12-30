<script setup>
import { ref, computed } from 'vue';
import Card from './components/Card.vue';
const items = ref([
  {
    id: 1,
    name: 'アボカドディップバケット',
    description: '刻んだ野菜をアボカドと混ぜてディップに。こんがり焼いたバゲットとお召し上がりください。',
    price: 480,
    image: '/images/item1.jpg',
    soldOut: false,
    selected: false,
  },
  {
    id: 2,
    name: 'あの日夢見たホットケーキ',
    description: '子供のころに食べたかった、あのホットケーキを再現しました。素朴でどこか懐かしい味をどうぞ。',
    price: 1180,
    image: '/images/item2.jpg',
    soldOut: false,
    selected: false,
  },
  {
    id: 3,
    name: 'HOP WTR',
    description: 'ロサンゼルス生まれのスパークリングウォーター。ノンカロリー、ノンアルコールの新感覚飲料です。',
    price: 320,
    image: '/images/item3.jpg',
    soldOut: true,
    selected: false,
  },
  {
    id: 4,
    name: 'チーズフレンチフライ',
    description: 'イタリア産チーズをたっぷりかけたアツアツのフレンチフライ。みんな大好きな一品です。',
    price: 670,
    image: '/images/item4.jpg',
    soldOut: false,
    selected: false,
  },
]);

const stockQuantityComputed = computed(() => {
  return items.value.filter((item) => item.soldOut === false).length;
});
const getDateComputed = computed(function () {
  return Date.now();
});

/**
 * 在庫のある商品数を返す
 */
function stockQuantity() {
  return items.value.filter((item) => item.soldOut === false).length;
}

/**
 * 商品の在庫状況を変更する
 * @param {object} item 商品情報
 */
function stockItem(item) {
  item.soldOut = false;
}

/**
 * 現在時刻を返す
 */
function getDate() {
  return Date.now();
}
</script>

<template>
  <header class="header">
    <img alt="" class="logo" src="/images/logo.svg" />
    <h1>Vue.js ハンズオン</h1>
  </header>
  <div>商品数: {{ stockQuantityComputed }}</div>
  <div>現在時刻: {{ getDate() }}</div>
  <div>現在時刻(computed)：{{ getDateComputed }}</div>
  <main class="main">
    <template v-for="item in items" :key="item.id">
      <div
        v-if="!item.soldOut"
        class="item"
        :class="{ selectedItem: item.selected }"
        @click="item.selected = !item.selected"
        @keyup.enter="item.selected = !item.selected"
        tabindex="0"
      >
        <Card :name="item.name" :description="item.description" :price="item.price" :image="item.image" />
      </div>
      <div v-else> 売り切れです<button type="button" @click="stockItem(item)">入荷</button> </div>
    </template>
  </main>
</template>

<style scoped>
body {
  font-family: sans-serif;
  margin: 0;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#app {
  width: 90%;
  margin: 0 5%;
  color: #242424;
}

.header {
  display: flex;
  align-content: center;
  align-items: center;
  margin-top: 40px;
  margin-bottom: 40px;
}

.header > img {
  width: 100px;
  height: 100px;
  margin-right: 20px;
}

.header > h1 {
  font-size: 80px;
  font-weight: bold;
  line-height: 80px;
  margin-top: 0;
  margin-bottom: 0;
}

.main {
  display: grid;
  grid-template-columns: 3fr 3fr 3fr 3fr;
  column-gap: 24px;
  row-gap: 24px;
}

.selectedItem {
  border: 2px solid #e3f2fd;
}
</style>
