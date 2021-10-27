<template>
  <div class="wrapper w-1/5">
    <div class="w-full flex flex-col">
      <div
        class="drag-drawflow"
        draggable="true"
        ondragstart="drag(event)"
        data-node="facebook"
      >
        <span> Number</span>
      </div>
      <div
        class="drag-drawflow"
        draggable="true"
        ondragstart="drag(event)"
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
        ondragstart="drag(event)"
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
