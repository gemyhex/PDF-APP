<template>
  <form class="form" @submit.prevent="UploadFiles">
    <div class="mb-3">
      <label for="company_name" class="form-label">Company Name</label>
      <input
        type="text"
        class="form-control"
        id="company_name"
        placeholder="Company Name"
      />
    </div>
    <div class="mb-3">
      <label for="formFileMultiple" class="form-label">PDF Files</label>
      <input
        class="form-control"
        type="file"
        multiple
        required
        @change="onFileChange"
        accept=".pdf,.doc"
        ref="pdfs"
      />
    </div>
    <div class="mb-3 text-center">
      <button type="submit" class="btn btn-primary">Send &amp; Compare</button>
    </div>
  </form>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      pdfs: [],
      url: "https://pdf.smarttechno.co/api/pdf",
    };
  },
  methods: {
    onFileChange(event) {
      // let pdfs = this.$refs.files.files;
      this.pdfs = event.target.files;
      console.log(this.pdfs);
    },
    async UploadFiles() {
      const formData = new FormData();
      for (var i = 0; i < this.$refs.pdfs.files.length; i++) {
        let file = this.$refs.pdfs.files[i];
        formData.append("pdfs[" + i + "]", file);
      }
      const headers = { "Content-Type": "multipart/form-data" };
      axios
        .post(this.url, formData, { headers })
        .then((res) => {
          // res.data.result.forEach((element, i) => {
          //   console.log("elements: ", i + 1);
          // });
          this.$store.state.headlines = res.data.result.length;
        })
        .catch(console.error);
    },
  },
};
</script>

<style>
.form {
  width: 600px;
  margin: 20px auto;
  background: #eee;
  padding: 10px;
  border-radius: 8px;
}
.box {
  width: 100%;
  min-height: 10px;
}
</style>
