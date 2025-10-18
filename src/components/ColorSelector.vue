<template>
  <div>
    <div>
      <h3>色1を選択</h3>
      <div class="colors">
        <div
          v-for="color in colors"
          :key="color.name"
          :style="{ backgroundColor: color.code }"
          class="color-box"
          :class="{ selected: selectedColor1 === color.name }"
          @click="selectColor('color1', color.name, color.code)"
        ></div>
      </div>
      <p class="selected-color-display" :style="{ backgroundColor: selectedColor1Code }">
        選択された色1: {{ selectedColor1 || "未選択" }}
      </p>
    </div>

    <div>
      <h3>色2を選択</h3>
      <div class="colors">
        <div
          v-for="color in colors"
          :key="color.name"
          :style="{ backgroundColor: color.code }"
          class="color-box"
          :class="{ selected: selectedColor2 === color.name }"
          @click="selectColor('color2', color.name, color.code)"
        ></div>
      </div>
      <p class="selected-color-display" :style="{ backgroundColor: selectedColor2Code }">
        選択された色2: {{ selectedColor2 || "未選択" }}
      </p>
    </div>

    <button @click="emitSelection" :disabled="!selectedColor1 || !selectedColor2">
      検索
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      colors: [
        { name: "パステルブルー", code: "#49BDF0" },
        { name: "エメラルドグリーン", code: "#00a968" },
        { name: "グリーン", code: "#00a960" },
        { name: "パールグリーン", code: "#98fb98" },
        { name: "ライトグリーン", code: "#90ee90" },
        { name: "イエロー", code: "#ffdc00" },
        { name: "オレンジ", code: "#ee7800" },
        { name: "レッド", code: "#ff0000" },
        { name: "ホワイト", code: "#ffffff" },
        { name: "サクラピンク", code: "#fceeeb" },
        { name: "ピンク", code: "#FFC0CB" },
        { name: "パッションピンク", code: "#fc0fc0" },
        { name: "バイオレット", code: "#5a4498" },
        { name: "パープル", code: "#9b72b0" },
        { name: "ブルー", code: "#0000ff" },
      ],
      selectedColor1: null,
      selectedColor1Code: "transparent",
      selectedColor2: null,
      selectedColor2Code: "transparent",
    };
  },
  methods: {
    selectColor(target, colorName, colorCode) {
      if (target === "color1") {
        this.selectedColor1 = this.selectedColor1 === colorName ? null : colorName;
        this.selectedColor1Code = this.selectedColor1 ? colorCode : "transparent";
      } else if (target === "color2") {
        this.selectedColor2 = this.selectedColor2 === colorName ? null : colorName;
        this.selectedColor2Code = this.selectedColor2 ? colorCode : "transparent";
      }
    },
    emitSelection() {
      this.$emit("selectCombination", [this.selectedColor1, this.selectedColor2]);
    },
  },
};
</script>


<style>
.colors {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 10px;
  justify-content: center;
}
.color-box {
  width: 50px;
  height: 50px;
  border-radius: 5px;
  border: 2px solid transparent;
  cursor: pointer;
  transition: transform 0.2s, border 0.2s;
}
.color-box:hover {
  transform: scale(1.1);
  border: 2px solid #aaa;
}
.selected {
  border: 3px solid #333;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
}
.selected-color-display {
  display: inline-block;
  padding: 5px 15px;
  margin-top: 5px;
  border-radius: 5px;
  font-weight: bold;
  color: white;
  border: 1px solid #ccc;
  text-shadow:
    -1px -1px 0 black,
     1px -1px 0 black,
    -1px  1px 0 black,
     1px  1px 0 black;
}
button {
  margin-top: 10px;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  background-color: #007BFF;
  color: white;
  border: none;
  border-radius: 5px;
}
button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

@media (min-width: 440px) {
  #app {
    margin-left: 33%;
    margin-bottom: 20%;
    padding: 10px;
  }
}
</style>
