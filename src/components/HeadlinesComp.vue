<template>
  <div class="list">
    <div class="drag-zone">
      <drag v-for="(n, i) in head" :data="n" :class="'item' + i" :key="n.id">
        <HeadlineComp
          :title="n.title"
          :content="n.content"
          :id="n.id"
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
          <drag class="item" :key="item.id">{{ item.title }}</drag>
        </template>
        <template v-slot:feedback="{ data }">
          <div class="item feedback" :key="data.id">{{ data.title }}</div>
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
    },
  },
};
</script>

<style scoped>
.list {
  border: 1px solid black;
  margin: 100px auto;
  width: 600px;
  display: flex;
}

.item {
  padding: 10px;
  margin: 10px;
  width: fit-content;
  background-color: rgb(220, 220, 255);
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
