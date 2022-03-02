<template>
  <div class="list col">
    <div class="row">
      <div class="drag-zone col">
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
          ></HeadlineComp>
        </drag>
      </div>
      <div class="drop-zone col">
        <button class="btn btn-primary mt-1">Next File</button>
        <drop-list
          :items="items"
          class="list drop-box"
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
      indx: 0,
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
  /* display: flex; */
}
.drop-box {
  min-height: 100%;
  flex-direction: column;
}
.item {
  max-width: 100%;
  padding: 2px;
  margin: 2px;
  text-overflow: ellipsis;
}
.draggable {
  background: lightgreen;
  padding: 8px;
}
.dnd-drop {
  height: 100vh;
  max-height: 100vh;
  margin: 10px;
  overflow-y: inherit;
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
.drop-zone {
  border: 1px solid green;
}
</style>
