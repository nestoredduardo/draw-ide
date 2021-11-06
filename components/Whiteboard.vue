<template>
  <section class="flex whiteboard">
    <button
      class="
        absolute
        z-10
        bg-blue-200
        font-bold
        text-5xl
        rounded-full
        w-14
        h-14
        flex
        justify-center
        align-center
        bottom-20
        right-10
        sm:hidden
      "
      @click="showAside"
    >
      +
    </button>

    <div v-if="displayAside" class="w-1/3 sm:w-1/5 right-1/3 sm:block">
      <div class="w-full flex flex-col">
        <div
          class="drag-drawflow"
          draggable="true"
          @dragstart="drag($event)"
          @touchend="drop($event)"
          data-node="number"
        >
          <span> Number</span>
        </div>
        <div
          class="drag-drawflow"
          draggable="true"
          @dragstart="drag($event)"
          @touchend="drop($event)"
          data-node="assign"
        >
          <span> Assign </span>
        </div>
        <div
          class="drag-drawflow"
          draggable="true"
          @dragstart="drag($event)"
          @touchend="drop($event)"
          data-node="print"
        >
          <span> Print</span>
        </div>
        <div
          class="drag-drawflow"
          draggable="true"
          @dragstart="drag($event)"
          @touchstart="drag($event)"
          @touchend="drop($event)"
          data-node="add"
        >
          <span> Add</span>
        </div>
        <div
          class="drag-drawflow"
          draggable="true"
          @dragstart="drag($event)"
          @touchend="drop($event)"
          data-node="substrack"
        >
          <span> Substrack</span>
        </div>
        <div
          class="drag-drawflow"
          draggable="true"
          @dragstart="drag($event)"
          @touchend="drop($event)"
          data-node="multiply"
        >
          <span> Multiply </span>
        </div>
        <div
          class="drag-drawflow"
          draggable="true"
          @dragstart="drag($event)"
          @touchend="drop($event)"
          data-node="divide"
        >
          <span> Divide</span>
        </div>
        <div
          class="drag-drawflow"
          draggable="true"
          @dragstart="drag($event)"
          @touchend="drop($event)"
          data-node="ifelse"
        >
          <span> If - Else</span>
        </div>
        <div
          class="drag-drawflow"
          draggable="true"
          @dragstart="drag($event)"
          @touchend="drop($event)"
          data-node="for"
        >
          <span> For Bucle</span>
        </div>
        <div
          class="drag-drawflow"
          draggable="true"
          @dragstart="drag($event)"
          @touchend="drop($event)"
          data-node="end"
        >
          <span> End Block </span>
        </div>
        <div class="hidden px-6 text-center py-4 text-xl sm:block">
          Made with ☕ by
          <a
            href="https://twitter.com/nestoredduardo"
            target="_blank"
            class="text-blue-500"
            >@nestoredduardo</a
          >
        </div>
      </div>
    </div>
    <div
      id="drawflow"
      class="h-full"
      @dragover.prevent
      @dragenter.prevent
      @drop="drop($event)"
    ></div>
  </section>
</template>

<script>
import Vue from "vue";
import NodeClick from "./NodeClick.vue";
import Drawflow from "drawflow";
import styleDrawflow from "drawflow/dist/drawflow.min.css";

import Number from "./Nodes/Number.vue";
import Assign from "./Nodes/Assign.vue";
import Print from "./Nodes/Print.vue";
import Add from "./Nodes/Add";
import Substrack from "./Nodes/Substrack.vue";
import Multiply from "./Nodes/Multiply.vue";
import Divide from "./Nodes/Divide.vue";
import IfElse from "./Nodes/IfElse.vue";
import For from "./Nodes/For.vue";
import End from "./Nodes/End.vue";

export default {
  name: "App",
  data() {
    return {
      editor: null,
      displayAside: true,
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

    //Events
    this.editor.on("nodeCreated", function (id) {
      console.log("Node created " + id);
    });

    this.editor.on("nodeRemoved", function (id) {
      console.log("Node removed " + id);
    });

    this.editor.on("nodeSelected", function (id) {
      console.log("Node selected " + id);
    });

    this.editor.on("moduleCreated", function (name) {
      console.log("Module Created " + name);
    });

    this.editor.on("moduleChanged", function (name) {
      console.log("Module Changed " + name);
    });

    this.editor.on("connectionCreated", function (connection) {
      console.log("Connection created");
      console.log(connection);
    });

    this.editor.on("connectionRemoved", function (connection) {
      console.log("Connection removed");
      console.log(connection);
    });

    this.editor.on("mouseMove", function (position) {
      console.log("Position mouse x:" + position.x + " y:" + position.y);
    });

    this.editor.on("nodeMoved", function (id) {
      console.log("Node moved " + id);
    });

    this.editor.on("zoom", function (zoom) {
      console.log("Zoom level " + zoom);
    });

    this.editor.on("translate", function (position) {
      console.log("Translate x:" + position.x + " y:" + position.y);
    });

    this.editor.on("addReroute", function (id) {
      console.log("Reroute added " + id);
    });

    this.editor.on("removeReroute", function (id) {
      console.log("Reroute removed " + id);
    });

    function positionMobile(ev) {
      const mobile_last_move = ev;
    }

    var transform = "";
    function showpopup(e) {
      e.target.closest(".drawflow-node").style.zIndex = "9999";
      e.target.children[0].style.display = "block";
      //document.getElementById("modalfix").style.display = "block";

      //e.target.children[0].style.transform = 'translate('+translate.x+'px, '+translate.y+'px)';
      transform = editor.precanvas.style.transform;
      this.editor.precanvas.style.transform = "";
      this.editor.precanvas.style.left = editor.canvas_x + "px";
      this.editor.precanvas.style.top = editor.canvas_y + "px";
      console.log(transform);

      //e.target.children[0].style.top  =  -editor.canvas_y - editor.container.offsetTop +'px';
      //e.target.children[0].style.left  =  -editor.canvas_x  - editor.container.offsetLeft +'px';
      this.editor.editor_mode = "fixed";
    }

    function closemodal(e) {
      e.target.closest(".drawflow-node").style.zIndex = "2";
      e.target.parentElement.parentElement.style.display = "none";
      //document.getElementById("modalfix").style.display = "none";
      this.editor.precanvas.style.transform = transform;
      this.editor.precanvas.style.left = "0px";
      this.editor.precanvas.style.top = "0px";
      this.editor.editor_mode = "edit";
    }

    function changeModule(event) {
      var all = document.querySelectorAll(".menu ul li");
      for (var i = 0; i < all.length; i++) {
        all[i].classList.remove("selected");
      }
      event.target.classList.add("selected");
    }

    function changeMode(option) {
      //console.log(lock.id);
      if (option == "lock") {
        lock.style.display = "none";
        unlock.style.display = "block";
      } else {
        lock.style.display = "block";
        unlock.style.display = "none";
      }
    }
  },
  data() {
    return {
      mobile_item_selec: "",
      mobile_last_move: null,
      displayAside: true,
    };
  },
  methods: {
    exportData() {
      alert(JSON.stringify(this.editor.export()));
    },
    showAside() {
      this.displayAside = !this.displayAside;
    },
    positionMobile(ev) {
      const mobile_last_move = ev;
    },

    allowDrop(ev) {
      ev.preventDefault();
    },

    drag(ev) {
      console.log(ev);
      if (ev.type === "touchstart") {
        const mobile_item_selec = ev.target
          .closest(".drag-drawflow")
          .getAttribute("data-node");
      } else {
        ev.dataTransfer.setData("node", ev.target.getAttribute("data-node"));
      }
    },
    drop(ev) {
      console.log(ev);
      const mobile_last_move = ev;
      let mobile_item_selec;
      if (ev.target.closest(".drag-drawflow") !== null) {
        mobile_item_selec = ev.target
          .closest(".drag-drawflow")
          .getAttribute("data-node");
      }

      if (ev.type === "touchend") {
        const touches =
          mobile_last_move.touches[0] || mobile_last_move.changedTouches[0];
        var parentdrawflow = document
          .elementFromPoint(touches.clientX, touches.clientY)
          .closest("#drawflow");
        if (parentdrawflow != null) {
          this.addNodeToDrawFlow(
            mobile_item_selec,
            touches.clientX,
            touches.clientY
          );
        }
        mobile_item_selec = "";
      } else {
        ev.preventDefault();
        var data = ev.dataTransfer.getData("node");
        this.addNodeToDrawFlow(data, ev.clientX, ev.clientY);
      }
    },
    addNodeToDrawFlow(name, pos_x, pos_y) {
      if (this.editor.editor_mode === "fixed") {
        return false;
      }
      pos_x =
        pos_x *
          (this.editor.precanvas.clientWidth /
            (this.editor.precanvas.clientWidth * this.editor.zoom)) -
        this.editor.precanvas.getBoundingClientRect().x *
          (this.editor.precanvas.clientWidth /
            (this.editor.precanvas.clientWidth * this.editor.zoom));
      pos_y =
        pos_y *
          (this.editor.precanvas.clientHeight /
            (this.editor.precanvas.clientHeight * this.editor.zoom)) -
        this.editor.precanvas.getBoundingClientRect().y *
          (this.editor.precanvas.clientHeight /
            (this.editor.precanvas.clientHeight * this.editor.zoom));

      switch (name) {
        case "number":
          const props = {};
          const options = {};
          this.editor.registerNode("Number", Number, props, options);
          const data = {};
          //editor.addNode(name, inputs, outputs, posx, posy, class, data, html);
          this.editor.addNode(
            "Number",
            0,
            1,
            pos_x,
            pos_y,
            "Class",
            data,
            "Number",
            "vue"
          );
          break;
        case "assign":
          this.editor.registerNode("Assign", Assign, props, options);
          this.editor.addNode(
            "assign",
            1,
            1,
            pos_x,
            pos_y,
            "assign",
            {},
            "Assign",
            "vue"
          );
          break;
        case "print":
          this.editor.registerNode("Print", Print, props, options);
          this.editor.addNode(
            "print",
            1,
            1,
            pos_x,
            pos_y,
            "print",
            {},
            "Print",
            "vue"
          );
          break;
        case "add":
          this.editor.registerNode("Add", Add, props, options);
          this.editor.addNode(
            "add",
            2,
            1,
            pos_x,
            pos_y,
            "add",
            {},
            "Add",
            "vue"
          );
          break;
        case "substrack":
          this.editor.registerNode("Substrack", Substrack, props, options);
          this.editor.addNode(
            "substrack",
            2,
            1,
            pos_x,
            pos_y,
            "substrack",
            {},
            "Substrack",
            "vue"
          );
          break;
        case "multiply":
          this.editor.registerNode("Multiply", Multiply, props, options);
          this.editor.addNode(
            "multiply",
            2,
            1,
            pos_x,
            pos_y,
            "multiply",
            {},
            "Multiply",
            "vue"
          );
          break;
        case "divide":
          this.editor.registerNode("Divide", Divide, props, options);
          this.editor.addNode(
            "divide",
            2,
            1,
            pos_x,
            pos_y,
            "divide",
            {},
            "Divide",
            "vue"
          );
          break;
        case "ifelse":
          this.editor.registerNode("IfElse", IfElse, props, options);
          this.editor.addNode(
            "ifelse",
            2,
            2,
            pos_x,
            pos_y,
            "ifelse",
            {},
            "IfElse",
            "vue"
          );
          break;

        case "for":
          this.editor.registerNode("For", For, props, options);
          this.editor.addNode(
            "for",
            1,
            1,
            pos_x,
            pos_y,
            "for",
            {},
            "For",
            "vue"
          );
          break;
        case "end":
          this.editor.registerNode("End", End, props, options);
          this.editor.addNode(
            "end",
            1,
            1,
            pos_x,
            pos_y,
            "end",
            {},
            "End",
            "vue"
          );
          break;

        default:
      }
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

.whiteboard {
  height: calc(100vh - 150px);
}

@media screen and (min-width: 640px) {
  .whiteboard {
    height: calc(100vh - 104px);
  }
}

.wrapper {
  height: 100%;
  display: flex;
}

.drag-drawflow {
  font-size: 1.2rem;
  line-height: 50px;
  border-bottom: 1px solid rgba(229, 231, 235, 1);
  cursor: move;
  user-select: none;
  text-align: center;
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

  --dfNodeSelectedBackgroundColor: rgba(98, 165, 234, 1);
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
