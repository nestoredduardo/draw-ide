<template>
  <div class="wrapper w-1/5">
    <div class="w-full flex flex-col">
      <div
        class="drag-drawflow"
        draggable="true"
        v-on:ondragstart="drag(event)"
        @drop="drop(event)"
        data-node="facebook"
      >
        <span> Number</span>
      </div>
      <div
        class="drag-drawflow"
        draggable="true"
        v-on:ondragstart="drag(event)"
        data-node="slack"
      >
        <span> Assign </span>
      </div>
      <div
        class="drag-drawflow"
        draggable="true"
        ondragstart="drag(event)"
        data-node="github"
      >
        <span> Print</span>
      </div>
      <div
        class="drag-drawflow"
        draggable="true"
        ondragstart="drag(event)"
        data-node="telegram"
      >
        <span> Add</span>
      </div>
      <div
        class="drag-drawflow"
        draggable="true"
        ondragstart="drag(event)"
        data-node="aws"
      >
        <span> Substrack</span>
      </div>
      <div
        class="drag-drawflow"
        draggable="true"
        ondragstart="drag(event)"
        data-node="log"
      >
        <span> Multiply </span>
      </div>
      <div
        class="drag-drawflow"
        draggable="true"
        ondragstart="drag(event)"
        data-node="google"
      >
        <span> Divide</span>
      </div>
      <div
        class="drag-drawflow"
        draggable="true"
        @ondragstart="drag(event)"
        data-node="email"
      >
        <span> If - Else</span>
      </div>
      <div
        class="drag-drawflow"
        draggable="true"
        ondragstart="drag(event)"
        data-node="template"
      >
        <span> For Bucle</span>
      </div>
      <div class="px-6 text-center py-4 text-xl">
        Made with 💚 by
        <a
          href="https://twitter.com/nestoredduardo"
          target="_blank"
          class="text-blue-500"
          >@nestoredduardo</a
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    exportData() {
      alert(JSON.stringify(this.editor.export()));
    },
    drag: function (ev) {
      console.log("Drag");
      if (ev.type === "touchstart") {
        mobile_item_selec = ev.target
          .closest(".drag-drawflow")
          .getAttribute("data-node");
      } else {
        ev.dataTransfer.setData("node", ev.target.getAttribute("data-node"));
      }
    },
    drop(ev) {
      console.log("Drop done");
      if (ev.type === "touchend") {
        var parentdrawflow = document
          .elementFromPoint(
            mobile_last_move.touches[0].clientX,
            mobile_last_move.touches[0].clientY
          )
          .closest("#drawflow");
        if (parentdrawflow != null) {
          addNodeToDrawFlow(
            mobile_item_selec,
            mobile_last_move.touches[0].clientX,
            mobile_last_move.touches[0].clientY
          );
        }
        mobile_item_selec = "";
      } else {
        ev.preventDefault();
        var data = ev.dataTransfer.getData("node");
        addNodeToDrawFlow(data, ev.clientX, ev.clientY);
      }
    },
  },
};
</script>

<style>
.wrapper {
  height: 100%;
  display: flex;
}

.drag-drawflow {
  font-size: 1.2rem;
  line-height: 55px;
  border-bottom: 1px solid rgba(229, 231, 235, 1);
  cursor: move;
  user-select: none;
  text-align: center;
}
</style>
