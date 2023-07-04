<template>
  <div>
    <!-- <ul>
      <li
        v-for="node in tree"
        :key="node.id"
        :data-id="node.id"
        :draggable="true"
        @dragstart="dragStartHandler"
      >
        {{ node.label }}
        <ul v-if="node.children.length > 0">
          <li
            v-for="child in node.children"
            :key="child.id"
            :data-id="child.id"
            :draggable="true"
            @dragstart="dragStartHandler"
          >
            {{ child.label }}
          </li>
        </ul>
      </li>
    </ul> -->
    <!-- <draggable
      v-model="tree"
      group="people"
      @start="drag = true"
      @end="drag = false"
    >
      <div v-for="element in tree" :key="element.id">{{ element.label }}</div>
    </draggable> -->

    <draggable class="dragArea" tag="ul" :list="data" :group="{ name: 'g1' }">
      <li v-for="el in children" :key="el.name">
        <p>{{ el.name }}</p>
        <nested-draggable v-if="el.children" :tasks="el.children" />
      </li>
    </draggable>
  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "TestC",
  components: {
    draggable,
  },
  data() {
    return {
      tree: [
        {
          id: 1,
          label: "Node 1",
          children: [
            {
              id: 2,
              label: "Node 2",
              children: [],
            },
            {
              id: 3,
              label: "Node 3",
              children: [],
            },
          ],
        },
      ],
      dragData: null,
      structure: [
        { name: "Prelude" },
        { name: "Verse" },
        { name: "Middle", children: [{ name: "Chorus" }, { name: "Verse" }] },
        { name: "Last Chorus" },
      ],
    };
  },
  methods: {
    // dragStartHandler(event) {
    //   const nodeId = event.target.dataset.id;
    //   this.dragData = this.findNodeById(this.tree, nodeId);
    // },
    // findNodeById(nodes, nodeId) {
    //   for (const node of nodes) {
    //     if (node.id === nodeId) {
    //       return node;
    //     }
    //     const childNode = this.findNodeById(node.children, nodeId);
    //     if (childNode) {
    //       return childNode;
    //     }
    //   }
    //   return null;
    // },
  },
};
</script>
