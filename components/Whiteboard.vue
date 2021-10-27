<template>
  <div id="drawflow"></div>
</template>

<script>
import Vue from "vue";
import NodeClick from "./NodeClick.vue";
import Drawflow from "drawflow";
import styleDrawflow from "drawflow/dist/drawflow.min.css";

export default {
  name: "App",
  data() {
    return {
      editor: null,
    };
  },
  mounted() {
    const id = document.getElementById("drawflow");
    this.editor = new Drawflow(id, Vue);
    this.editor.start();
    const props = { name: "Hello user" };
    const options = {};
    this.editor.registerNode("NodeClick", NodeClick, props, options);
    const data = { name: "" };
    //editor.addNode(name, inputs, outputs, posx, posy, class, data, html);
    this.editor.addNode(
      "Name",
      0,
      1,
      150,
      300,
      "Class",
      data,
      "NodeClick",
      "vue"
    );
  },
  methods: {
    exportData() {
      alert(JSON.stringify(this.editor.export()));
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#drawflow {
  width: 100%;
  height: 500px;
  border: 1px solid red;
}
</style>
