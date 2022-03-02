<template>
  <div class="home container-fluid">
    <nav-bar @change="onChange($event)"></nav-bar>
    <div class="row page">
      <div class="col right-sec" v-if="!result">
        <div class="container">
          <div class="logo">
            <img src="@/assets/pdf.svg" alt="logo" />
            <div class="types">
              <h3>Welcome To PDF Compare</h3>
              <p>PDF Compare Is A Tool For Compare PDF Files.</p>
            </div>
          </div>
        </div>
      </div>
      <div class="col right-sec" v-else>
        <div class="content">
          <modal-comp>
            <div class="headlines row">
              <h2>
                {{ company ? company : "" }}
              </h2>
              <headlines-comp
                v-for="(head, i) in result"
                :key="i"
                :head="head"
              ></headlines-comp>
            </div>
          </modal-comp>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import HeadlinesComp from "@/components/HeadlinesComp.vue";
import ModalComp from "@/components/ModalComp.vue";
import NavBar from "@/components/NavBar.vue";
// @ is an alias to /src

export default {
  name: "HomeView",
  components: { HeadlinesComp, ModalComp, NavBar },
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
  position: relative;
  padding: 0;
  .page {
    width: 100%;
    min-height: calc(100vh - 60px);
    margin-top: 60px;
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
        width: 40%;
      }
    }
  }
  .headlines {
    h2 {
      text-align: center;
    }
  }
}
</style>
