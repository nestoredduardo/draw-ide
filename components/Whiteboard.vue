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
}

:root {
  --dfBackgroundColor: rgba(255, 255, 255, 1);
  --dfBackgroundSize: 30px;
  --dfBackgroundImage: linear-gradient(
      to right,
      rgba(225, 227, 234, 1) 1px,
      transparent 1px
    ),
    linear-gradient(to bottom, rgba(225, 227, 234, 1) 1px, transparent 1px);

  --dfNodeType: flex;
  --dfNodeTypeFloat: none;
  --dfNodeBackgroundColor: #ffffff;
  --dfNodeTextColor: #000000;
  --dfNodeBorderSize: 2px;
  --dfNodeBorderColor: rgba(140, 159, 237, 1);
  --dfNodeBorderRadius: 4px;
  --dfNodeMinHeight: 40px;
  --dfNodeMinWidth: 160px;
  --dfNodePaddingTop: 15px;
  --dfNodePaddingBottom: 15px;
  --dfNodeBoxShadowHL: 0px;
  --dfNodeBoxShadowVL: 0px;
  --dfNodeBoxShadowBR: 15px;
  --dfNodeBoxShadowS: 2px;
  --dfNodeBoxShadowColor: rgba(215, 207, 207, 1);

  --dfNodeHoverBackgroundColor: #ffffff;
  --dfNodeHoverTextColor: #000000;
  --dfNodeHoverBorderSize: 2px;
  --dfNodeHoverBorderColor: #000000;
  --dfNodeHoverBorderRadius: 4px;

  --dfNodeHoverBoxShadowHL: 0px;
  --dfNodeHoverBoxShadowVL: 2px;
  --dfNodeHoverBoxShadowBR: 15px;
  --dfNodeHoverBoxShadowS: 2px;
  --dfNodeHoverBoxShadowColor: #4ea9ff;

  --dfNodeSelectedBackgroundColor: rgba(234, 98, 192, 1);
  --dfNodeSelectedTextColor: #ffffff;
  --dfNodeSelectedBorderSize: 2px;
  --dfNodeSelectedBorderColor: rgba(21, 22, 112, 1);
  --dfNodeSelectedBorderRadius: 4px;

  --dfNodeSelectedBoxShadowHL: 0px;
  --dfNodeSelectedBoxShadowVL: 2px;
  --dfNodeSelectedBoxShadowBR: 15px;
  --dfNodeSelectedBoxShadowS: 2px;
  --dfNodeSelectedBoxShadowColor: #4ea9ff;

  --dfInputBackgroundColor: #ffffff;
  --dfInputBorderSize: 2px;
  --dfInputBorderColor: rgba(200, 204, 221, 1);
  --dfInputBorderRadius: 50px;
  --dfInputLeft: -27px;
  --dfInputHeight: 20px;
  --dfInputWidth: 20px;

  --dfInputHoverBackgroundColor: #ffffff;
  --dfInputHoverBorderSize: 2px;
  --dfInputHoverBorderColor: #000000;
  --dfInputHoverBorderRadius: 50px;

  --dfOutputBackgroundColor: #ffffff;
  --dfOutputBorderSize: 2px;
  --dfOutputBorderColor: rgba(200, 204, 221, 1);
  --dfOutputBorderRadius: 50px;
  --dfOutputRight: -3px;
  --dfOutputHeight: 20px;
  --dfOutputWidth: 20px;

  --dfOutputHoverBackgroundColor: #ffffff;
  --dfOutputHoverBorderSize: 2px;
  --dfOutputHoverBorderColor: #000000;
  --dfOutputHoverBorderRadius: 50px;

  --dfLineWidth: 3px;
  --dfLineColor: rgba(0, 128, 235, 1);
  --dfLineHoverColor: rgba(0, 128, 235, 1);
  --dfLineSelectedColor: rgba(254, 199, 59, 1);

  --dfRerouteBorderWidth: 2px;
  --dfRerouteBorderColor: #000000;
  --dfRerouteBackgroundColor: #ffffff;

  --dfRerouteHoverBorderWidth: 2px;
  --dfRerouteHoverBorderColor: #000000;
  --dfRerouteHoverBackgroundColor: #ffffff;

  --dfDeleteDisplay: block;
  --dfDeleteColor: #ffffff;
  --dfDeleteBackgroundColor: rgba(237, 73, 73, 1);
  --dfDeleteBorderSize: 2px;
  --dfDeleteBorderColor: #ffffff;
  --dfDeleteBorderRadius: 50px;
  --dfDeleteTop: -15px;

  --dfDeleteHoverColor: rgba(244, 243, 243, 1);
  --dfDeleteHoverBackgroundColor: rgba(255, 0, 0, 1);
  --dfDeleteHoverBorderSize: 2px;
  --dfDeleteHoverBorderColor: rgba(255, 255, 255, 1);
  --dfDeleteHoverBorderRadius: 50px;
}

#drawflow {
  background: var(--dfBackgroundColor);
  background-size: var(--dfBackgroundSize) var(--dfBackgroundSize);
  background-image: var(--dfBackgroundImage);
}

.drawflow .drawflow-node {
  display: var(--dfNodeType);
  background: var(--dfNodeBackgroundColor);
  color: var(--dfNodeTextColor);
  border: var(--dfNodeBorderSize) solid var(--dfNodeBorderColor);
  border-radius: var(--dfNodeBorderRadius);
  min-height: var(--dfNodeMinHeight);
  width: auto;
  min-width: var(--dfNodeMinWidth);
  padding-top: var(--dfNodePaddingTop);
  padding-bottom: var(--dfNodePaddingBottom);
  -webkit-box-shadow: var(--dfNodeBoxShadowHL) var(--dfNodeBoxShadowVL)
    var(--dfNodeBoxShadowBR) var(--dfNodeBoxShadowS) var(--dfNodeBoxShadowColor);
  box-shadow: var(--dfNodeBoxShadowHL) var(--dfNodeBoxShadowVL)
    var(--dfNodeBoxShadowBR) var(--dfNodeBoxShadowS) var(--dfNodeBoxShadowColor);
}

.drawflow .drawflow-node:hover {
  background: var(--dfNodeHoverBackgroundColor);
  color: var(--dfNodeHoverTextColor);
  border: var(--dfNodeHoverBorderSize) solid var(--dfNodeHoverBorderColor);
  border-radius: var(--dfNodeHoverBorderRadius);
  -webkit-box-shadow: var(--dfNodeHoverBoxShadowHL)
    var(--dfNodeHoverBoxShadowVL) var(--dfNodeHoverBoxShadowBR)
    var(--dfNodeHoverBoxShadowS) var(--dfNodeHoverBoxShadowColor);
  box-shadow: var(--dfNodeHoverBoxShadowHL) var(--dfNodeHoverBoxShadowVL)
    var(--dfNodeHoverBoxShadowBR) var(--dfNodeHoverBoxShadowS)
    var(--dfNodeHoverBoxShadowColor);
}

.drawflow .drawflow-node.selected {
  background: var(--dfNodeSelectedBackgroundColor);
  color: var(--dfNodeSelectedTextColor);
  border: var(--dfNodeSelectedBorderSize) solid var(--dfNodeSelectedBorderColor);
  border-radius: var(--dfNodeSelectedBorderRadius);
  -webkit-box-shadow: var(--dfNodeSelectedBoxShadowHL)
    var(--dfNodeSelectedBoxShadowVL) var(--dfNodeSelectedBoxShadowBR)
    var(--dfNodeSelectedBoxShadowS) var(--dfNodeSelectedBoxShadowColor);
  box-shadow: var(--dfNodeSelectedBoxShadowHL) var(--dfNodeSelectedBoxShadowVL)
    var(--dfNodeSelectedBoxShadowBR) var(--dfNodeSelectedBoxShadowS)
    var(--dfNodeSelectedBoxShadowColor);
}

.drawflow .drawflow-node .input {
  left: var(--dfInputLeft);
  background: var(--dfInputBackgroundColor);
  border: var(--dfInputBorderSize) solid var(--dfInputBorderColor);
  border-radius: var(--dfInputBorderRadius);
  height: var(--dfInputHeight);
  width: var(--dfInputWidth);
}

.drawflow .drawflow-node .input:hover {
  background: var(--dfInputHoverBackgroundColor);
  border: var(--dfInputHoverBorderSize) solid var(--dfInputHoverBorderColor);
  border-radius: var(--dfInputHoverBorderRadius);
}

.drawflow .drawflow-node .outputs {
  float: var(--dfNodeTypeFloat);
}

.drawflow .drawflow-node .output {
  right: var(--dfOutputRight);
  background: var(--dfOutputBackgroundColor);
  border: var(--dfOutputBorderSize) solid var(--dfOutputBorderColor);
  border-radius: var(--dfOutputBorderRadius);
  height: var(--dfOutputHeight);
  width: var(--dfOutputWidth);
}

.drawflow .drawflow-node .output:hover {
  background: var(--dfOutputHoverBackgroundColor);
  border: var(--dfOutputHoverBorderSize) solid var(--dfOutputHoverBorderColor);
  border-radius: var(--dfOutputHoverBorderRadius);
}

.drawflow .connection .main-path {
  stroke-width: var(--dfLineWidth);
  stroke: var(--dfLineColor);
}

.drawflow .connection .main-path:hover {
  stroke: var(--dfLineHoverColor);
}

.drawflow .connection .main-path.selected {
  stroke: var(--dfLineSelectedColor);
}

.drawflow .connection .point {
  stroke: var(--dfRerouteBorderColor);
  stroke-width: var(--dfRerouteBorderWidth);
  fill: var(--dfRerouteBackgroundColor);
}

.drawflow .connection .point:hover {
  stroke: var(--dfRerouteHoverBorderColor);
  stroke-width: var(--dfRerouteHoverBorderWidth);
  fill: var(--dfRerouteHoverBackgroundColor);
}

.drawflow-delete {
  display: var(--dfDeleteDisplay);
  color: var(--dfDeleteColor);
  background: var(--dfDeleteBackgroundColor);
  border: var(--dfDeleteBorderSize) solid var(--dfDeleteBorderColor);
  border-radius: var(--dfDeleteBorderRadius);
}

.parent-node .drawflow-delete {
  top: var(--dfDeleteTop);
}

.drawflow-delete:hover {
  color: var(--dfDeleteHoverColor);
  background: var(--dfDeleteHoverBackgroundColor);
  border: var(--dfDeleteHoverBorderSize) solid var(--dfDeleteHoverBorderColor);
  border-radius: var(--dfDeleteHoverBorderRadius);
}
</style>
