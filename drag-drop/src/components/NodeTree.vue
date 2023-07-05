<template>
  <div class="node-tree">
    <div class="node-tree-main">
      <h1>Change orientation</h1>
      <select v-model="treeOrientation" style="margin-bottom: 20px">
        <option value="0">Vertical</option>
        <option value="1">Horizontal</option>
      </select>
      <!-- <p>This is Node tree component</p> -->
      <h1>Tree</h1>
      <div>
        <blocks-tree
          :data="treeData"
          :horizontal="treeOrientation == '1'"
          :collapsable="true"
          :label-class-name="labelClassName"
          @dragstart="dragStart($event)"
          @drop="drop($event)"
          @dragenter.prevent
          @dragover.prevent
        ></blocks-tree>
        <!-- <draggable
          v-model="myArray"
          group="people"
          @start="drag = true"
          @end="drag = false"
        >
          <div v-for="element in myArray" :key="element.id">
            {{ element.name }}
          </div>
        </draggable> -->
        <!-- <div
          style="
            border: 1px solid black;
            height: 50px;
            width: 50px;
            margin: 10px auto;
          "
          @drop="drop($event)"
          @dragenter.prevent
          @dragover.prevent
        ></div> -->
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
import { reactive, ref } from "vue";
// import VueBlocksTree from "vue3-blocks-tree";
// import nestedDraggable from ""
// import draggable from "vuedraggable";

export default {
  name: "NodeTree",
  components: {
    // draggable,
  },
  data() {
    return {
      // selected: ref([]),
      treeOrientation: ref("0"),
      // drag: true,
      treeData: reactive({
        label: "root1",
        expand: true,
        some_id: 1,
        parentId: null,
        key: this.some_id,
        // drag: true,
        // ondragstart: "dragStart(event)",
        children: [
          // { label: "child 1", some_id: 2 },
          // { label: "child 2", some_id: 3 },
          {
            label: "child2",
            some_id: 2,
            parentId: this.some_id,
            expand: false,
            // drag: true,
            children: [
              // { label: "subchild 1", some_id: 5 },
              {
                label: "child4",
                some_id: 4,
                expand: false,
                // draggable: true,
                children: [
                  { label: "child8", some_id: 8 },
                  { label: "child9", some_id: 9 },
                ],
              },
              {
                label: "child5",
                some_id: 5,
                expand: false,
                // draggable: true,
                children: [
                  { label: "child10", some_id: 10 },
                  { label: "child11", some_id: 11 },
                ],
              },
            ],
          },
          {
            label: "child3",
            some_id: 3,
            expand: false,
            // draggable: true,
            children: [
              // { label: "subchild 1", some_id: 5 },
              {
                label: "child6",
                some_id: 6,
                expand: false,
                // draggable: true,
                children: [
                  { label: "child12", some_id: 12 },
                  { label: "child13", some_id: 13 },
                ],
              },
              {
                label: "child7",
                some_id: 7,
                expand: false,
                // draggable: true,
                children: [
                  { label: "child14", some_id: 14 },
                  { label: "child15", some_id: 15 },
                ],
              },
            ],
          },
        ],
      }),
      labelClassName: this.some_id,
      id: this.treeData,
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
      // myArray: [
      //   { name: "Prelude", id: 0 },
      //   { name: "Verse", id: 1 },
      //   {
      //     name: "Middle",
      //     id: 2,
      //     children: [{ name: "Chorus" }, { name: "Verse" }],
      //   },
      //   { name: "Last Chorus", id: 3 },
      // ],
      up: "",
    };
  },
  methods: {
    dragStart(event) {
      console.log("Drag start..", event);
      // console.log(data);
      // console.log(this.id);
      // console.log(event.srcElement.outerText);
      // event.preventDefault();
      // event.dataTransfer.setData("Text", event.target.id);
      // console.log("...", this.$emit.setData("Text", this.treeData.label));
      // let a =
      event.dataTransfer.dropEffect = "move";
      event.dataTransfer.effectAllowed = "move";
      // console.log("....", event.target);
      event.dataTransfer.setData("text", event.srcElement.innerText);
      // event.dataTransfer.setData("text", event.srcElement.outerText);
      // console.log(this.text);
      // event.srcElement.innerHTML = this.dropLabel;
      this.up = event;
      // console.log(this.up);
      // console.log("Drag start..", event);
    },
    drop(event) {
      console.log("drop works..", event);
      // console.log(this.some_id);
      // console.log(this.treeData.some_id);
      // console.log(this.treeData.label);
      // this.label = this.treeData.label;
      console.log("....", event.dataTransfer.getData("text"));
      let dragLabel = event.dataTransfer.getData("text");
      console.log("dragLabel...", dragLabel);
      let dropLabel = event.srcElement.innerText;
      console.log("dropLabel..", dropLabel);
      let temp = dragLabel;
      dragLabel = dropLabel;
      dropLabel = temp;
      console.log("drag", dragLabel + " drop", dropLabel + " temp", temp);
      // console.log("drop", dropLabel);
      // console.log("temp", temp);

      // let inner = event.srcElement.innerHTML;
      event.srcElement.innerHTML = dropLabel;
      this.up.srcElement.innerText = null;
      // dragStart1(){
      //   event.srcElement.innerHTML = dragLabel;
      // }

      // console.log("inner");
      // event.target.appendChild(document.getElementById(dragLabel));
      // console.log((this.treeData.label = dragLabel));
      // const item = this.treeData.find((item) => item.label == itemId);
      // item.this.treeData.label = this.treeData.label;
    },
    // nodeClick() {
    //   console.log("clicked....");

    // },
  },
};
</script>

<style scoped>
::v-deep .org-tree-node-label {
  -webkit-user-drag: element;
  user-select: none;
}
</style>
