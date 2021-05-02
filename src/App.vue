<template>
  <div id="App">
    <div id="headingDiv">
      <button id="bold" @click="handleHeading(1)">h1</button>
      <button id="bold" @click="handleHeading(2)">h2</button>
      <button id="bold" @click="handleHeading(3)">h3</button>
      <button id="bold" @click="handleHeading(4)">h4</button>
      <button id="bold" @click="handleHeading(5)">h5</button>
      <button id="bold" @click="handleHeading(6)">h6</button>
    </div>
    <div id="editorDiv">
      <div id="editorWindow">
        <textarea id="editor" v-model="inputText"></textarea>
      </div>
      <div id="displayWindow">
        <div id="display" v-html="stylizedMarkdown"></div>
      </div>
    </div>
  </div>
</template>

<script>
import marked from "marked";
import DOMPurify from "dompurify";

export default {
  name: "App",
  components: {},
  data: () => {
    return {
      inputText: "# This is an h1",
    };
  },
  computed: {
    stylizedMarkdown() {
      let output = DOMPurify.sanitize(marked(this.inputText));
      console.log(output);
      return output;
    },
  },
  methods: {
    handleHeading(size) {
      console.log("#" * size);
      this.inputText = this.inputText + "#".repeat(size) + " ";
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;

  #editorDiv {
    display: flex;
  }

  #editorWindow,
  #displayWindow {
    width: 50%;
    height: 100vh;
  }

  #displayWindow {
    background-color: #f5f5f5;
    padding-left: 1rem;
    border-radius: 2%;
  }

  #editorWindow {
    margin-right: 1rem;

    #editor {
      border: none;
      height: 100vh;
      width: 99%;
      resize: none;
      font-size: 1.25rem;
      border-radius: 2%;
    }
  }
}
</style>
