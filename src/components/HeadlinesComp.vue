<template>
  <div class="list">
    <div class="drag-zone">
      <drag
        v-for="(con, idx, i) in head"
        :data="{ idx, con }"
        class="item"
        :key="idx"
      >
        <HeadlineComp
          :title="idx"
          :content="con"
          :id="`${idx.slice(0, 3).trim() + i}`"
          class="item"
        ></HeadlineComp>
      </drag>
    </div>
    <div class="drop-zone">
      <drop-list
        :items="items"
        class="list"
        @insert="onInsert"
        @reorder="$event.apply(items)"
      >
        <template v-slot:item="{ item }">
          <drag class="item draggable" :key="item.idx">{{ item.idx }}</drag>
        </template>
        <template v-slot:feedback="{ data }">
          <div class="item feedback" :key="data.idx">{{ data.idx }}</div>
        </template>
      </drop-list>
    </div>
  </div>
</template>

<script>
import { Drag, DropList } from "vue-easy-dnd";
import HeadlineComp from "@/components/HeadlineComp.vue";

export default {
  name: "App",
  components: {
    Drag,
    DropList,
    HeadlineComp,
  },
  props: ["head"],
  data() {
    return {
      items: [],
    };
  },
  methods: {
    onInsert(event) {
      this.items.splice(event.index, 0, event.data);
      console.log(this.items);
    },
  },
};
</script>

<style scoped>
.list {
  border: 1px solid black;
  margin: 100px auto;
  min-width: 500px;
}
.item {
  padding: 2px;
  margin: 2px;
}
.draggable {
  background: lightgreen;
  padding: 8px;
}
.dnd-drop {
  min-width: 100px;
  min-height: 100px;
  margin: 10px;
}
.item.feedback {
  background-color: rgb(255, 220, 220);
  border: 2px dashed black;
}

.item.drag-image {
  background-color: rgb(220, 255, 220);
  transform: translate(-50%, -50%);
}
.drag-zone {
}
</style>
