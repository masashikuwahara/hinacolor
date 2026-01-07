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
        'イエロー-パステルブルー': { name: '金村美玖', img: 'https://cdn.hinatazaka46.com/images/14/0f8/aa8dbc0edabe45368031be6c79492/800_800_102400.jpg' },
        'バイオレット-ホワイト': { name: '小坂菜緒', img: 'https://cdn.hinatazaka46.com/images/14/e96/64a2bafa84fdd35dd0b436e535348/800_800_102400.jpg' },
        'サクラピンク-パールグリーン': { name: '松田好花', img: 'https://cdn.hinatazaka46.com/images/14/797/97d4adf5917b888076c79a5b8e50e/800_800_102400.jpg' },
        'エメラルドグリーン-レッド': { name: '上村ひなの', img: 'https://cdn.hinatazaka46.com/images/14/d04/9a8fe13f4636d8ca094adb4f9726e/800_800_102400.jpg' },
        'グリーン-パープル': { name: '髙橋未来虹', img: 'https://cdn.hinatazaka46.com/images/14/d34/4927ef132fb234361a518f97e369d/800_800_102400.jpg' },
        'オレンジ-ブルー': { name: '森本茉莉', img: 'https://cdn.hinatazaka46.com/images/14/1e3/48fcdd30cf477f27f93a21a6b6dd8/800_800_102400.jpg' },
        'イエロー-パールグリーン': { name: '山口陽世', img: 'https://cdn.hinatazaka46.com/images/14/fed/5df39f1b192930fee694173c600f0/800_800_102400.jpg' },
        'オレンジ-サクラピンク': { name: '石塚瑶季', img: 'https://cdn.hinatazaka46.com/images/14/6ef/94cf9c2b6f3254dce52494c4f4925/800_800_102400.jpg' },
        'パープル-ブルー': { name: '小西夏菜実', img: 'https://cdn.hinatazaka46.com/images/14/827/757404acbe92864d153817acb12e0/800_800_102400.jpg' },
        'パステルブルー-ピンク': { name: '清水理央', img: 'https://cdn.hinatazaka46.com/images/14/1d6/385624baf3cd18f3f4d7709fcb6f7/800_800_102400.jpg' },
        'オレンジ-レッド': { name: '正源司陽子', img: 'https://cdn.hinatazaka46.com/images/14/74e/ebfcb3a5f10ed852335cb2172ebec/800_800_102400.jpg' },
        'イエロー-レッド': { name: '竹内希来里', img: 'https://cdn.hinatazaka46.com/images/14/543/a0e493c0270a6757baa8b4a54c52e/800_800_102400.jpg' },
        'オレンジ-パステルブルー': { name: '平尾帆夏', img: 'https://cdn.hinatazaka46.com/images/14/bf5/bd726453f34d3d133d9bb0d3bae0c/800_800_102400.jpg' },
        'イエロー-ブルー': { name: '平岡海月', img: 'https://cdn.hinatazaka46.com/images/14/956/ac38f15f5656b78b1341f8fb6a028/800_800_102400.jpg' },
        'サクラピンク-ブルー': { name: '藤嶌果歩', img: 'https://cdn.hinatazaka46.com/images/14/fb7/4074ff96e2c41ae13615c9861118b/800_800_102400.jpg' },
        'バイオレット-レッド': { name: '宮地すみれ', img: 'https://cdn.hinatazaka46.com/images/14/275/21cfa2f15b51c5bc4af0a176770da/800_800_102400.jpg' },
        'エメラルドグリーン-ホワイト': { name: '山下葉留花', img: 'https://cdn.hinatazaka46.com/images/14/f41/4a8eabba27e31011b513be1b464ca/800_800_102400.jpg' },
        'ブルー-ホワイト': { name: '渡辺莉奈', img: 'https://cdn.hinatazaka46.com/images/14/fd4/fcc2d6a008ca2e5734fa78a2a1010/800_800_102400.jpg' },
        'サクラピンク-ピンク': { name: '大田美月', img: 'https://cdn.hinatazaka46.com/images/14/10c/8419990a3e524e45906d43870ba73/800_800_102400.jpg' },
        'レッド-レッド': { name: '大野愛実', img: 'https://cdn.hinatazaka46.com/images/14/3e3/b7820aaa689ee4ee5f05c2c0a3031/800_800_102400.jpg' },
        'パステルブルー-パステルブルー': { name: '片山紗希', img: 'https://cdn.hinatazaka46.com/images/14/d26/478d286661b35c072d39ee43816d3/800_800_102400.jpg' },
        'サクラピンク-レッド': { name: '蔵盛妃那乃', img: 'https://cdn.hinatazaka46.com/images/14/8cb/1d6c0466c2a7d563c4e058c29b217/800_800_102400.jpg' },
        'ホワイト-ホワイト': { name: '坂井新奈', img: 'https://cdn.hinatazaka46.com/images/14/bbb/f1892edb55d2730f713aa01798c2c/800_800_102400.jpg' },
        'エメラルドグリーン-エメラルドグリーン': { name: '佐藤優羽', img: 'https://cdn.hinatazaka46.com/images/14/3dd/e4729797e5c1780c27a0c008ac814/800_800_102400.jpg' },
        'パステルブル-エメラルドグリーン': { name: '下田衣珠季', img: 'https://cdn.hinatazaka46.com/images/14/b47/9ae06a5dacf77719550757a1cfbdb/800_800_102400.jpg' },
        'パープル-イエロー': { name: '高井俐香', img: 'https://cdn.hinatazaka46.com/images/14/df1/1f43ebd9dda159fe4776239dc769b/800_800_102400.jpg' },
        'イエロー-オレンジ': { name: '鶴崎仁香', img: 'https://cdn.hinatazaka46.com/images/14/8a9/65fe0c09a4abe4023e2f98f917e80/800_800_102400.jpg' },
        'サクラピンク-ホワイト': { name: '松尾桜', img: 'https://cdn.hinatazaka46.com/images/14/282/6b6351372bdc873e897152790c45a/800_800_102400.jpg' }
      };
      this.result = combinations[combination] || { name: '組み合わせ無し', img: 'https://cdn.hinatazaka46.com/images/14/98b/e96b48f630edc3119806a1b40bc10/400_1080_102400.jpg' };
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
