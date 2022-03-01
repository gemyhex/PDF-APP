<template>
  <div class="home container-fluid">
    <div class="row page">
      <div class="col-4 left-sec">
        <div class="container">
          <form-comp @change="onChange($event)"></form-comp>
        </div>
      </div>
      <div class="col-8 right-sec">
        <div class="container">
          <img src="@/assets/pdf.svg" alt="logo" />
          <div class="logo"></div>
        </div>
      </div>
    </div>
    <div class="row overlay" v-if="result">
      <modal-comp>
        <div class="content">
          <div class="headlines">
            <h2 class="text-center">
              {{ company ? company : "" }}
            </h2>
            <headlines-comp
              v-for="(head, i) in result"
              :key="i"
              :head="head"
            ></headlines-comp>
          </div>
        </div>
      </modal-comp>
    </div>
  </div>
</template>

<script>
import FormComp from "@/components/FormComp.vue";
import HeadlinesComp from "@/components/HeadlinesComp.vue";
import ModalComp from "@/components/ModalComp.vue";
// @ is an alias to /src

export default {
  name: "HomeView",
  components: { FormComp, HeadlinesComp, ModalComp },
  methods: {
    onChange(res) {
      this.result = res.result;
      this.company = res.company;
    },
  },
  data() {
    return {
      result: null,
      company: "",
      loading: false,
    };
  },
};
</script>

<style lang="scss" scoped>
.home {
  max-width: 100vw;
  height: 100vh;
  position: relative;
  padding: 0;
  .page {
    width: 100%;
    min-height: 100vh;
    margin: 0;
    padding: 0;
    .right-sec,
    .left-sec {
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 0;
      .contanier {
        padding: 0;
      }
    }
    .right-sec {
      background: rgba(216, 182, 182, 0.486);
      img {
        width: 400px;
      }
    }
  }
  .overlay {
    width: 100%;
    height: 100%;
    background: red;
    position: absolute;
    top: 0;
    left: 0;
    padding: 0;
  }
  .headlines {
    display: flex;
  }
}
</style>
