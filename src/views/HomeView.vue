<template>
  <div class="home container-fluid">
    <nav-bar @onChange="onChange($event)"></nav-bar>
    <div class="page">
      <div class="right-sec" v-if="!result">
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
      <div class="right-sec" v-else>
        <div class="container">
          <div class="row mt-3">
            <button
              type="button"
              class="btn btn-primary"
              data-bs-toggle="modal"
              data-bs-target="#exampleModal"
            >
              Show Table
            </button>
          </div>
          <div class="content row mt-3">
            <HeadlinesComp
              v-for="(file, ind) in result"
              :key="ind"
              :result="file"
              class="col hline"
            ></HeadlinesComp>
          </div>
        </div>
      </div>
      <!-- Modal -->
      <div
        class="modal fade"
        id="exampleModal"
        tabindex="-1"
        aria-labelledby="exampleModalLabel"
        aria-hidden="true"
      >
        <div class="modal-dialog modal-fullscreen">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel">Final Table</h5>
              <button
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
                aria-label="Close"
              ></button>
            </div>
            <div class="modal-body">
              <table class="tableC table-bordered"></table>
            </div>
            <div class="modal-footer">
              <button
                @click="GetTheFile"
                class="btn btn-success"
                data-bs-dismiss="modal"
                aria-label="Close"
              >
                Create PDF
              </button>
              <button
                @click="EmptyTable"
                class="btn btn-danger"
                data-bs-dismiss="modal"
                aria-label="Close"
              >
                Clear Table
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import HeadlinesComp from "@/components/HeadlinesComp.vue";
import NavBar from "@/components/NavBar.vue";
// @ is an alias to /src
import { jsPDF } from "jspdf";
export default {
  name: "HomeView",
  components: { HeadlinesComp, NavBar },
  data() {
    return {
      result: null,
      company: "",
      table_raw: "",
      loading: false,
    };
  },
  methods: {
    onChange(res) {
      this.result = res;
      this.company = res;
    },
    onCreate(val) {
      console.log("emit: ", val);
    },
    EmptyTable() {
      let table = document.querySelector(".tableC");
      table.innerHTML = "";
    },
    GetTheFile() {
      var doc = new jsPDF({
        orientation: "p", // landscape
        unit: "pt", // points, pixels won't work properly
        format: [window.outerWidth, window.innerHeight], // set needed dimensions for any element
      });
      doc.setFontSize(12);
      let table = document.querySelector(".tableC");
      this.table_raw = table.innerHTML;

      doc.html(table, {
        callback: function (doc) {
          doc.save("Compare.pdf");
        },
        x: 10,
        y: 10,
        // autoPaging: "text",
      });
    },
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
    .right-sec {
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 0;
      min-height: calc(100vh - 60px);
      background: rgba(216, 182, 182, 0.486);
      .contanier {
        padding: 0;
      }
      img {
        width: 40%;
      }
      .hline:not(:last-child) {
        border-right: 2px solid green;
      }
    }
  }
}
</style>
