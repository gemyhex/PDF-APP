<template>
  <div class="home">
    <form-comp></form-comp>
    <div class="headlines" v-if="headlines">
      <headlines-comp
        v-for="(head, i) in headlines"
        :key="i"
        :head="head"
      ></headlines-comp>
    </div>
  </div>
</template>

<script>
import FormComp from "@/components/FormComp.vue";
import HeadlinesComp from "@/components/HeadlinesComp.vue";
// @ is an alias to /src

export default {
  name: "HomeView",
  components: { FormComp, HeadlinesComp },
  data() {
    return {
      headlines: {
        dragItems: [
          {
            id: 0,
            title: "Head",
            content: "Lorem100",
          },
          {
            id: 1,
            title: "Head",
            content: "Lorem100",
          },
          {
            id: 2,
            title: "Head",
            content: "Lorem100",
          },
        ],
      },
    };
  },
};
</script>
