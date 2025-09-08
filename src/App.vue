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
        'イエロー-パステルブルー': { name: '金村美玖', img: 'https://cdn.hinatazaka46.com/images/14/cbc/d1cb5ac751a0038704dcb1f03462f/800_800_102400.jpg' },
        'イエロー-サクラピンク': { name: '河田陽菜', img: 'https://cdn.hinatazaka46.com/images/14/b91/c85a566828c5b52b392ead7cb9d35/800_800_102400.jpg' },
        'バイオレット-ホワイト': { name: '小坂菜緒', img: 'https://cdn.hinatazaka46.com/images/14/a5b/07f4597c589bc06d3a9daf61c355a/800_800_102400.jpg' },
        'サクラピンク-パールグリーン': { name: '松田好花', img: 'https://cdn.hinatazaka46.com/images/14/5f6/8fff4d82a94f458f8e93ab2cd8bdc/800_800_102400.jpg' },
        'エメラルドグリーン-レッド': { name: '上村ひなの', img: 'https://cdn.hinatazaka46.com/images/14/f5a/11215aab89ddb4f3229fc10abbb3d/800_800_102400.jpg' },
        'グリーン-パープル': { name: '髙橋未来虹', img: 'https://cdn.hinatazaka46.com/images/14/7d0/0e90ce02923eb0cd872e2fa8d3f00/800_800_102400.jpg' },
        'オレンジ-ブルー': { name: '森本茉莉', img: 'https://cdn.hinatazaka46.com/images/14/abc/8bab66b616bdc2da0d70ac7e9793f/800_800_102400.jpg' },
        'イエロー-パールグリーン': { name: '山口陽世', img: 'https://cdn.hinatazaka46.com/images/14/f08/9749323f550c0a3576e6b0cb2fe8b/800_800_102400.jpg' },
        'オレンジ-サクラピンク': { name: '石塚瑶季', img: 'https://cdn.hinatazaka46.com/images/14/1ad/5ac47cabb38c185c0048973531d26/800_800_102400.jpg' },
        'パープル-ブルー': { name: '小西夏菜実', img: 'https://cdn.hinatazaka46.com/images/14/02d/7472616773e47e0b00af1d73fe0a0/800_800_102400.jpg' },
        'パステルブルー-ピンク': { name: '清水理央', img: 'https://cdn.hinatazaka46.com/images/14/b0a/2ac28754d5f9965bc864182b8d35d/800_800_102400.jpg' },
        'オレンジ-レッド': { name: '正源司陽子', img: 'https://cdn.hinatazaka46.com/images/14/58b/b8c0350612a2ab0d73290b58df49c/800_800_102400.jpg' },
        'イエロー-レッド': { name: '竹内希来里', img: 'https://cdn.hinatazaka46.com/images/14/db3/b0ef9dd99d5d161d5c6a74ccded88/800_800_102400.jpg' },
        'オレンジ-パステルブルー': { name: '平尾帆夏', img: 'https://cdn.hinatazaka46.com/images/14/b94/d6fb430765ba4e52e1dff3770ca74/800_800_102400.jpg' },
        'イエロー-ブルー': { name: '平岡海月', img: 'https://cdn.hinatazaka46.com/images/14/371/9264a91c28a52a627b6431b53bc6b/800_800_102400.jpg' },
        'サクラピンク-ブルー': { name: '藤嶌果歩', img: 'https://cdn.hinatazaka46.com/images/14/d93/562a91de03cf903757a8c78fdf0de/800_800_102400.jpg' },
        'バイオレット-レッド': { name: '宮地すみれ', img: 'https://cdn.hinatazaka46.com/images/14/ed9/4bf9b8c45c896fc82510b36fef853/800_800_102400.jpg' },
        'エメラルドグリーン-ホワイト': { name: '山下葉留花', img: 'https://cdn.hinatazaka46.com/images/14/239/c487339f2d9093124c05f45fdf7a2/800_800_102400.jpg' },
        'ブルー-ホワイト': { name: '渡辺莉奈', img: 'https://cdn.hinatazaka46.com/images/14/4c4/b90f140e1bfddda84b099083159c1/800_800_102400.jpg' },
        'サクラピンク-ピンク': { name: '大田美月', img: 'https://cdn.hinatazaka46.com/images/14/325/4c87d9c8e738b16a035a9a8ac174d/800_800_102400.jpg' },
        'レッド-レッド': { name: '大野愛実', img: 'https://cdn.hinatazaka46.com/images/14/db5/593ef57f48945415097679c838dbc/800_800_102400.jpg' },
        'パステルブルー-パステルブルー': { name: '片山紗希', img: 'https://cdn.hinatazaka46.com/images/14/e92/c4ee448d69f4e440856329fc9dbec/800_800_102400.jpg' },
        'サクラピンク-レッド': { name: '蔵盛妃那乃', img: 'https://cdn.hinatazaka46.com/images/14/934/a5fde0c1aa6626255c888fc4a0a0f/800_800_102400.jpg' },
        'ホワイト-ホワイト': { name: '坂井新奈', img: 'https://cdn.hinatazaka46.com/images/14/0ef/f301c0034434b8d1124862e96cd32/800_800_102400.jpg' },
        'エメラルドグリーン-エメラルドグリーン': { name: '佐藤優羽', img: 'https://cdn.hinatazaka46.com/images/14/2f7/3d8d0410361f8237a311082a85cff/800_800_102400.jpg' },
        'パステルブル-エメラルドグリーン': { name: '下田衣珠季', img: 'https://cdn.hinatazaka46.com/images/14/7c2/d7eb3651cf3c905eec9fc62261fe1/800_800_102400.jpg' },
        'パープル-イエロー': { name: '高井俐香', img: 'https://cdn.hinatazaka46.com/images/14/962/d2eb46b321a8c8b15b0a588514344/800_800_102400.jpg' },
        'イエロー-オレンジ': { name: '鶴崎仁香', img: 'https://cdn.hinatazaka46.com/images/14/7ae/60b2e53359c77316cd7d490c337b7/800_800_102400.jpg' },
        'サクラピンク-ホワイト': { name: '松尾桜', img: 'https://cdn.hinatazaka46.com/images/14/fe4/1645f537167c2f6e7b3205fe0826e/800_800_102400.jpg' }
      };
      this.result = combinations[combination] || { name: '組み合わせ無し', img: 'https://cdn.hinatazaka46.com/images/14/e42/d1963a56c269c59003e420b3c8a3a/200_200_102400.jpg' };
    }
  }
};
</script>

<style>
body {
  background-color: #7cc7e8;
}

.app {
  font-family: "Helvetica Neue",Arial,"Hiragino Kaku Gothic ProN",
    "Hiragino Sans",Meiryo,sans-serif;
  text-align: center;
  color: #fff;
}
</style>
