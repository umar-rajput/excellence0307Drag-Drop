<template>
  <div class="node-tree">
    <div class="node-tree-main">
      <h1>Change orientation</h1>
      <select v-model="treeOrientation">
        <option value="0">Vertical</option>
        <option value="1">Horizontal</option>
      </select>
      <!-- <p>This is Node tree component</p> -->
      <h1>Basic</h1>
      <div>
        <blocks-tree
          :data="treeData"
          :horizontal="treeOrientation == '1'"
          :collapsable="true"
          :draggable="true"
          @dragstart="dragStart($event, treeData)"
          @drop="drop(event)"
          @dragenter.prevent
          @dragover.prevent
        ></blocks-tree>
        <div
          style="
            border: 1px solid black;
            height: 50px;
            width: 50px;
            margin: 10px auto;
          "
          @drop="drop($event)"
          @dragenter.prevent
          @dragover.prevent
        ></div>
      </div>
      <!-- <h1>With slots</h1>
      <div>
        <blocks-tree
          :data="treeData"
          :horizontal="treeOrientation == '1'"
          :collapsable="true"
        >
          <template #node="{ data, context }">
            <span>
              <input
                type="checkbox"
                :checked="selected.indexOf(data.some_id) > -1"
                @change="(e) => toggleSelect(data, e.target.checked)"
              />
              {{ data.label }}
            </span>
            <br />
            <span v-if="data.children && data.children.length">
              <a href="#" @click="context.toggleExpand">toggle expand</a>
            </span>
          </template>
        </blocks-tree>
        <div>Selected: {{ selected }}</div>
      </div> -->
    </div>
  </div>
</template>

<script>
import { ref, reactive } from "vue";
// import VueBlocksTree from "vue3-blocks-tree";

export default {
  name: "NodeTree",
  data() {
    return {
      selected: ref([]),
      treeOrientation: ref("0"),
      treeData: reactive({
        label: "root",
        expand: true,
        some_id: 1,
        // draggable: true,
        // ondragstart: "dragStart(event)",
        children: [
          // { label: "child 1", some_id: 2 },
          // { label: "child 2", some_id: 3 },
          {
            label: "subparent 1",
            some_id: 4,
            expand: false,
            // draggable: true,
            children: [
              // { label: "subchild 1", some_id: 5 },
              {
                label: "subchild 2",
                some_id: 6,
                expand: false,
                // draggable: true,
                children: [
                  { label: "subchild 11", some_id: 7 },
                  { label: "subchild 22", some_id: 8 },
                ],
              },
              {
                label: "subchild 2",
                some_id: 6,
                expand: false,
                // draggable: true,
                children: [
                  { label: "subchild 11", some_id: 7 },
                  { label: "subchild 22", some_id: 8 },
                ],
              },
            ],
          },
          {
            label: "subparent 1",
            some_id: 4,
            expand: false,
            // draggable: true,
            children: [
              // { label: "subchild 1", some_id: 5 },
              {
                label: "subchild 2",
                some_id: 6,
                expand: false,
                // draggable: true,
                children: [
                  { label: "subchild 11", some_id: 7 },
                  { label: "subchild 22", some_id: 8 },
                ],
              },
              {
                label: "subchild 2",
                some_id: 6,
                expand: false,
                // draggable: true,
                children: [
                  { label: "subchild 11", some_id: 7 },
                  { label: "subchild 22", some_id: 8 },
                ],
              },
            ],
          },
        ],
      }),
      // toggleSelect: (node, isSelected) => {
      //   isSelected
      //     ? this.selected.value.push(node.some_id)
      //     : this.selected.value.splice(
      //         this.selected.value.indexOf(node.some_id),
      //         1
      //       );
      //   if (node.children && node.children.length) {
      //     node.children.forEach((ch) => {
      //       this.toggleSelect(ch, isSelected);
      //     });
      //   }
      // },
    };
  },
  methods: {
    dragStart(event) {
      console.log("Drag start..", event);
      // event.dataTransfer.setData("Text", event.target.id);
      // console.log("...", this.$emit.setData("Text", this.treeData.label));
      console.log(
        "...."
        // event.dataTransfer.setData("text", this.treeData.label)
      );
      console.log("Drag start..", event);
    },
    drop(event) {
      console.log("drop works..", event);
      // console.log(this.some_id);
      console.log(this.treeData.some_id);
      console.log(this.treeData.label);
      // this.label = this.treeData.label;
      // console.log("....", event.dataTransfer.getData("text"));
      // const itemId = event.dataTransfer.getData("text");
      // const item = this.treeData.find((item) => item.label == itemId);
      // item.this.treeData.label = this.treeData.label;
    },
  },
};
</script>

<style scoped></style>
