<template>
  <div>
    <h1>Props warning Formatter</h1>
    <br />

    <textarea
      id="w3review"
      name="w3review"
      rows="10"
      cols="50"
      v-model="inputText"
    />
    <div />

    <textarea
      id="w3review"
      name="w3review"
      rows="10"
      cols="50"
      v-model="outputText"
    />
  </div>
</template>

<script>
export default {
  name: "About",
  data() {
    return {
      inputText: ``,
      outputText: "",
    };
  },
  watch: {
    inputText(newVal, oldVal) {
      let p = newVal;
      let formattedText = "";
      let label = p.trim().split(":")[0].trim();
      let arrayValue = p.trim().split(":")[1].trim();
      let word = "";
      let listOfWords = [];
      let listOfWordsIndex = 0;
      for (let i = 0; i < arrayValue.length; i++) {
        let codeOfChar = arrayValue.charCodeAt(i);
        if (
          (codeOfChar >= 97 && codeOfChar <= 122) ||
          (codeOfChar <= 90 && codeOfChar >= 65)
        ) {
          word += arrayValue[i];
        } else {
          if (word) {
            listOfWords[listOfWordsIndex++] = word;
          }
          word = "";
        }
      }
      arrayValue = listOfWords;
      let o = "";
      for (let i = 0; i < arrayValue.length; i++) {
        o += `${arrayValue[i]}: {
    type: Boolean,
    default: false,
  }`;
        o += `,`;
      }
      formattedText = `${label}: { ${o} },`;
      this.outputText = formattedText;
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
