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
    ※ペンライトカラー及びメンバーは2025年4月現在の情報です
  </p>
  <br>
  Ver.1.2.1
</template>

<script>
export default {
  data(){
    return {
      histories: [
        { date: '2025.04.08', content: '清水理央と渡辺莉奈のカラー変更'},
        { date: '2025.03.13', content: '選択した色を表示する機能の追加'},
        { date: '2025.01.28', content: '卒業メンバーを削除しました'},
        { date: '2024.12.18', content: 'リリースしました'}
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
