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
        'イエロー-パステルブルー': { name: '金村美玖', img: 'https://cdn.hinatazaka46.com/images/14/2c2/c3ae8953ee146fdadfe44d85012e9/800_800_102400.jpg' },
        'イエロー-サクラピンク': { name: '河田陽菜', img: 'https://cdn.hinatazaka46.com/images/14/411/32bbd7c5164b39ea39661824f4e21/800_800_102400.jpg' },
        'バイオレット-ホワイト': { name: '小坂菜緒', img: 'https://cdn.hinatazaka46.com/images/14/986/ec2f3f08b66935e6ba01b63cd45a7/800_800_102400.jpg' },
        'パープル-パープル': { name: '富田鈴花', img: 'https://cdn.hinatazaka46.com/images/14/a3d/3354f4c554914640f4017cd4a1fa8/800_800_102400.jpg' },
        'サクラピンク-パールグリーン': { name: '松田好花', img: 'https://cdn.hinatazaka46.com/images/14/e8b/e6b0df96226daf1f06767800ca7ee/800_800_102400.jpg' },
        'エメラルドグリーン-レッド': { name: '上村ひなの', img: 'https://cdn.hinatazaka46.com/images/14/0bc/8d6fdde59e7a869b5eb3e8cbbb9ec/800_800_102400.jpg' },
        'グリーン-パープル': { name: '髙橋未来虹', img: 'https://cdn.hinatazaka46.com/images/14/742/584a21bc26ffe15adcd90d1f71995/800_800_102400.jpg' },
        'オレンジ-ブルー': { name: '森本茉莉', img: 'https://cdn.hinatazaka46.com/images/14/ee9/36456b0d5ff5746c13d413430c060/800_800_102400.jpg' },
        'イエロー-パールグリーン': { name: '山口陽世', img: 'https://cdn.hinatazaka46.com/images/14/12e/0a07ce1751542f2adaffc4864c2d8/800_800_102400.jpg' },
        'オレンジ-サクラピンク': { name: '石塚瑶季', img: 'https://cdn.hinatazaka46.com/images/14/b6b/7531866cbfdc9e45771b207c663b9/800_800_102400.jpg' },
        'パープル-ブルー': { name: '小西夏菜実', img: 'https://cdn.hinatazaka46.com/images/14/be3/e7afdb38158eff2b52b083a76add5/800_800_102400.jpg' },
        'パステルブルー-ピンク': { name: '清水理央', img: 'https://cdn.hinatazaka46.com/images/14/0cd/622d5b4525423dad8acc3eaa55184/800_800_102400.jpg' },
        'オレンジ-レッド': { name: '正源司陽子', img: 'https://cdn.hinatazaka46.com/images/14/069/b12ad29e18865e254262d65f669d4/800_800_102400.jpg' },
        'イエロー-レッド': { name: '竹内希来里', img: 'https://cdn.hinatazaka46.com/images/14/b9a/e4ecf4bf46bea83f7879dedd4ded1/800_800_102400.jpg' },
        'オレンジ-パステルブルー': { name: '平尾帆夏', img: 'https://cdn.hinatazaka46.com/images/14/e9c/589d937f3322fbfd5348f82583999/800_800_102400.jpg' },
        'イエロー-ブルー': { name: '平岡海月', img: 'https://cdn.hinatazaka46.com/images/14/216/8efc4cf58743acf595b5378422f70/800_800_102400.jpg' },
        'サクラピンク-ブルー': { name: '藤嶌果歩', img: 'https://cdn.hinatazaka46.com/images/14/be2/549d2480910f7aee27d3b41e1177b/800_800_102400.jpg' },
        'バイオレット-レッド': { name: '宮地すみれ', img: 'https://cdn.hinatazaka46.com/images/14/36c/6d74ffab3174730fd7d0733b6fe59/800_800_102400.jpg' },
        'エメラルドグリーン-ホワイト': { name: '山下葉留花', img: 'https://cdn.hinatazaka46.com/images/14/1b8/f227907cdd3cf50bf93259f350f35/800_800_102400.jpg' },
        'ブルー-ホワイト': { name: '渡辺莉奈', img: 'https://cdn.hinatazaka46.com/images/14/3dd/7b622e22d226dc3af3055ba047d62/800_800_102400.jpg' },
        'サクラピンク-ピンク': { name: '大田美月', img: 'https://cdn.hinatazaka46.com/images/14/0b2/db47d067b57a9133f7400d1bcefb9/800_800_102400.jpg' },
        'レッド-レッド': { name: '大野愛実', img: 'https://cdn.hinatazaka46.com/images/14/eaf/8ae9d93ca626e3ab7e3ed6f2645bb/800_800_102400.jpg' },
        'パステルブルー-パステルブルー': { name: '片山紗希', img: 'https://cdn.hinatazaka46.com/images/14/7aa/00f105e430ed11d0b85d781e5726c/800_800_102400.jpg' },
        'サクラピンク-レッド': { name: '蔵盛妃那乃', img: 'https://cdn.hinatazaka46.com/images/14/6d3/cfcc1cd4c2fce8c85d866c233662a/800_800_102400.jpg' },
        'ホワイト-ホワイト': { name: '坂井新奈', img: 'https://cdn.hinatazaka46.com/images/14/805/b6aa8c6f51a79188f88e9a1730cd7/800_800_102400.jpg' },
        'エメラルドグリーン-エメラルドグリーン': { name: '佐藤優羽', img: 'https://cdn.hinatazaka46.com/images/14/a1b/53d31007ada309f447747a7106d95/800_800_102400.jpg' },
        'パステルブル-エメラルドグリーン': { name: '下田衣珠季', img: 'https://cdn.hinatazaka46.com/images/14/974/67a87660396dd40211a4f5d181268/800_800_102400.jpg' },
        'パープル-イエロー': { name: '高井俐香', img: 'https://cdn.hinatazaka46.com/images/14/36b/4f7bb6dac2d27f99e1751b1c8b002/800_800_102400.jpg' },
        'イエロー-オレンジ': { name: '鶴崎仁香', img: 'https://cdn.hinatazaka46.com/images/14/b6b/09af1fde4fda44ce8ae1d3f647bc4/800_800_102400.jpg' },
        'サクラピンク-ホワイト': { name: '松尾桜', img: 'https://cdn.hinatazaka46.com/images/14/157/8ed522d3a392e136e67aa69275ef9/800_800_102400.jpg' }
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
