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
        'ブルー-ブルー': { name: '加藤史帆', img: 'https://cdn.hinatazaka46.com/images/14/610/d713c2e65eee8fa173ef6c62d0d49/800_800_102400.jpg' },
        'パステルブルー-パープル': { name: '佐々木久美', img: 'https://cdn.hinatazaka46.com/images/14/ee4/c440e836d7b07df8aefc0b84ab181/800_800_102400.jpg' },
        'イエロー-イエロー': { name: '佐々木美玲', img: 'https://cdn.hinatazaka46.com/images/14/235/7c13d7b8915d31edbe0325581728d/800_800_102400.jpg' },
        'ピンク-ホワイト': { name: '高瀬愛奈', img: 'https://cdn.hinatazaka46.com/images/14/192/fd8942dc6d3234f5e3218201955a9/800_800_102400.jpg' },
        'サクラピンク-サクラピンク': { name: '東村芽依', img: 'https://cdn.hinatazaka46.com/images/14/e8d/6d3443d32d21af5b4250cae4dfe98/800_800_102400.jpg' },
        'イエロー-パステルブルー': { name: '金村美玖', img: 'https://cdn.hinatazaka46.com/images/14/884/f4b546a892ac328b9c50c546e9a8b/800_800_102400.jpg' },
        'イエロー-サクラピンク': { name: '河田陽菜', img: 'https://cdn.hinatazaka46.com/images/14/bfe/73bebf9ac0ba7d4b4aad96a2cea80/800_800_102400.jpg' },
        'バイオレット-ホワイト': { name: '小坂菜緒', img: 'https://cdn.hinatazaka46.com/images/14/4ef/7eac8ec151107a9de955beaf7329a/800_800_102400.jpg' },
        'パープル-パープル': { name: '富田鈴花', img: 'https://cdn.hinatazaka46.com/images/14/f4c/60526d1d91e8d440a5e8c9047fc0e/400_320_102400.jpg' },
        'オレンジ-オレンジ': { name: '丹生明里', img: 'https://cdn.hinatazaka46.com/images/14/9bd/04f076fd4bb2a2133af488e5a4732/400_320_102400.jpg' },
        'オレンジ-ホワイト': { name: '濱岸ひより', img: 'https://cdn.hinatazaka46.com/images/14/afc/00d2a3192ea32e11b16094ab3eff5/400_320_102400.jpg' },
        'サクラピンク-パールグリーン': { name: '松田好花', img: 'https://cdn.hinatazaka46.com/images/14/eb4/2dfbfe8d46a69460fc9f16888acb4/400_320_102400.jpg' },
        'エメラルドグリーン-レッド': { name: '上村ひなの', img: 'https://cdn.hinatazaka46.com/images/14/f93/c946abc18313af6ecabf728050f4b/400_320_102400.jpg' },
        'グリーン-パープル': { name: '髙橋未来虹', img: 'https://cdn.hinatazaka46.com/images/14/eb8/35660b17030be73ffbbfb41555b72/400_320_102400.jpg' },
        'オレンジ-ブルー': { name: '森本茉莉', img: 'https://cdn.hinatazaka46.com/images/14/937/25b018046acd1e646e856c6369e9b/400_320_102400.jpg' },
        'イエロー-パールグリーン': { name: '山口陽世', img: 'https://cdn.hinatazaka46.com/images/14/bcc/cfb92e43a263000b242439e485fd0/400_320_102400.jpg' },
        'オレンジ-サクラピンク': { name: '石塚瑶季', img: 'https://cdn.hinatazaka46.com/images/14/a86/e1f789a190060837b09fa82076e2a/800_800_102400.jpg' },
        'パープル-ブルー': { name: '小西夏菜実', img: 'https://cdn.hinatazaka46.com/images/14/eaf/3b49b29c292f09ed71bb8649a9e12/400_320_102400.jpg' },
        'オレンジ-パールグリーン': { name: '清水理央', img: 'https://cdn.hinatazaka46.com/images/14/74d/4b397480fd172844cbcc5bacfe5e7/400_320_102400.jpg' },
        'オレンジ-レッド': { name: '正源司陽子', img: 'https://cdn.hinatazaka46.com/images/14/f02/6406ed92a0d1a7769fc2561dfcc68/400_320_102400.jpg' },
        'イエロー-レッド': { name: '竹内希来里', img: 'https://cdn.hinatazaka46.com/images/14/f81/9e69fa3e1130d66af7f867156616b/400_320_102400.jpg' },
        'オレンジ-パステルブルー': { name: '平尾帆夏', img: 'https://cdn.hinatazaka46.com/images/14/660/2cf7f6f78adf856981934c3dc479e/400_320_102400.jpg' },
        'イエロー-ブルー': { name: '平岡海月', img: 'https://cdn.hinatazaka46.com/images/14/71d/a3bcbe403190ec3c9725084518ee3/400_320_102400.jpg' },
        'サクラピンク-ブルー': { name: '藤嶌果歩', img: 'https://cdn.hinatazaka46.com/images/14/0a7/035fb647cd649e349d4fa75d4184e/400_320_102400.jpg' },
        'バイオレット-レッド': { name: '宮地すみれ', img: 'https://cdn.hinatazaka46.com/images/14/c33/92e4f5413e4613cd436b978e4e56a/400_320_102400.jpg' },
        'エメラルドグリーン-ホワイト': { name: '山下葉留花', img: 'https://cdn.hinatazaka46.com/images/14/ec6/d2b4bb358013dc930382899d74f98/400_320_102400.jpg' },
        'パープル-ピンク': { name: '渡辺莉奈', img: 'https://cdn.hinatazaka46.com/images/14/d33/b748daecd841a480ba4dce08eca48/400_320_102400.jpg' }
      };
      this.result = combinations[combination] || { name: '組み合わせ無し', img: 'https://cdn.hinatazaka46.com/images/14/760/4b421a6dd5d6e1f278f3651a39723/200_200_102400.jpg' };
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
