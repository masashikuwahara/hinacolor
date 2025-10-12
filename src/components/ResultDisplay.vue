<template>
  <div v-if="result">
    <p>{{ result.name }}</p>
    <img v-if="result.img" :src="result.img" alt="結果画像" />
  </div>
  <br>
  -更新履歴-<br>
  <div v-for="history in histories">
    {{ history.date }} {{ history.content }}
  </div>
  <p class="description">
    ※ペンライトカラー及びメンバーは2025年9月現在の情報です
  </p>
  <br>
  Ver.2.0.0
</template>

<script>
export default {
  data(){
    return {
      histories: [
        { date: '2025.09.07', content: '富田鈴花を削除、メンバー画像を変更'},
        { date: '2025.05.09', content: 'メンバー画像を変更'},
        { date: '2025.05.09', content: '五期生を追加'},
        { date: '2024.12.18', content: 'リリース'}
      ],
    }
  },
  props: {
    result: Object
  }
};
</script>
<style>
.description {
  font-size: 10px;
}

img {
  width: 300px;
}
</style>
