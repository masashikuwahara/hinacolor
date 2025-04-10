<template>
  <div class="app">
    <h1>HINACOLOR</h1>
    <p>日向坂46メンバーのペンライトカラーをメンバーではなく色から検索するちょっと変わったアプリです</p>
    <ColorSelector @selectCombination="getCombinationResult" />
    <ResultDisplay :result="result" />
  </div>
</template>

<script>
import ColorSelector from './components/ColorSelector.vue';
import ResultDisplay from './components/ResultDisplay.vue';

export default {
  components: { ColorSelector, ResultDisplay },
  data() {
    return {
      result: null
    };
  },
  methods: {
    getCombinationResult(selectedColors) {
      const combination = selectedColors.sort().join('-');
      const combinations = {
        'ピンク-ホワイト': { name: '高瀬愛奈', img: 'https://cdn.hinatazaka46.com/images/14/ccb/7cc864c9f0c54e8d7cc27c88cd6a1/800_800_102400.jpg' },
        'イエロー-パステルブルー': { name: '金村美玖', img: 'https://cdn.hinatazaka46.com/images/14/e3d/10e0ec44b93be391c4ab7f7e3cf0b/400_320_102400.jpg' },
        'イエロー-サクラピンク': { name: '河田陽菜', img: 'https://cdn.hinatazaka46.com/images/14/45b/c47ef916e2e0bf5e49a0144179153/400_320_102400.jpg' },
        'バイオレット-ホワイト': { name: '小坂菜緒', img: 'https://cdn.hinatazaka46.com/images/14/985/072c23fa8e0ac974f353d51d6d566/400_320_102400.jpg' },
        'パープル-パープル': { name: '富田鈴花', img: 'https://cdn.hinatazaka46.com/images/14/42f/2e3b0b500456d48a46514eceb343d/400_320_102400.jpg' },
        'サクラピンク-パールグリーン': { name: '松田好花', img: 'https://cdn.hinatazaka46.com/images/14/9c5/87d50e7853595aaefc3d14ab80749/400_320_102400.jpg' },
        'エメラルドグリーン-レッド': { name: '上村ひなの', img: 'https://cdn.hinatazaka46.com/images/14/9de/8d4bfed193adf56953f7aa3625760/400_320_102400.jpg' },
        'グリーン-パープル': { name: '髙橋未来虹', img: 'https://cdn.hinatazaka46.com/images/14/f8f/4112a6932e8751737def6f738abee/400_320_102400.jpg' },
        'オレンジ-ブルー': { name: '森本茉莉', img: 'https://cdn.hinatazaka46.com/images/14/65f/6ca2ac061bcda8026fb0a5aa9c804/400_320_102400.jpg' },
        'イエロー-パールグリーン': { name: '山口陽世', img: 'https://cdn.hinatazaka46.com/images/14/ebc/846dca80d22fbdb2dbf42f24ff5d9/400_320_102400.jpg' },
        'オレンジ-サクラピンク': { name: '石塚瑶季', img: 'https://cdn.hinatazaka46.com/images/14/b56/49ce8fef3670b03d97ed6b4212486/400_320_102400.jpg' },
        'パープル-ブルー': { name: '小西夏菜実', img: 'https://cdn.hinatazaka46.com/images/14/7af/4b0f4d4f5c906d391afea8edc8d25/400_320_102400.jpg' },
        'パステルブルー-ピンク': { name: '清水理央', img: 'https://cdn.hinatazaka46.com/images/14/b00/62d7047d19b84cc1b2922e011e2bf/400_320_102400.jpg' },
        'オレンジ-レッド': { name: '正源司陽子', img: 'https://cdn.hinatazaka46.com/images/14/9b4/914eced5b352a11d009eafedfefbc/400_320_102400.jpg' },
        'イエロー-レッド': { name: '竹内希来里', img: 'https://cdn.hinatazaka46.com/images/14/66d/c4f27cba509510a6f48c23a9ece1c/400_320_102400.jpg' },
        'オレンジ-パステルブルー': { name: '平尾帆夏', img: 'https://cdn.hinatazaka46.com/images/14/1de/576523c0628298356025a2193ecb0/400_320_102400.jpg' },
        'イエロー-ブルー': { name: '平岡海月', img: 'https://cdn.hinatazaka46.com/images/14/c86/d4f17e3172581f7855fd835f89f90/400_320_102400.jpg' },
        'サクラピンク-ブルー': { name: '藤嶌果歩', img: 'https://cdn.hinatazaka46.com/images/14/e39/7a5d6767ae33af1a7319529c461b5/400_320_102400.jpg' },
        'バイオレット-レッド': { name: '宮地すみれ', img: 'https://cdn.hinatazaka46.com/images/14/fa2/dbc520dc2a261472c591987a0a3ae/400_320_102400.jpg' },
        'エメラルドグリーン-ホワイト': { name: '山下葉留花', img: 'https://cdn.hinatazaka46.com/images/14/f25/16be8f588b8407199f992e5721915/400_320_102400.jpg' },
        'ブルー-ホワイト': { name: '渡辺莉奈', img: 'https://cdn.hinatazaka46.com/images/14/249/c9216245dc6e1bb429ca60ef175bb/400_320_102400.jpg' }
      };
      this.result = combinations[combination] || { name: '組み合わせ無し', img: 'https://cdn.hinatazaka46.com/images/14/cee/fdd9ce5600c3e28449d817494f466/200_200_102400.jpg' };
    }
  }
};
</script>

<style>
.app {
  font-family: 'Courier New', Courier, monospace;
  text-align: center;
  color: #7cc7e8;
}
</style>
