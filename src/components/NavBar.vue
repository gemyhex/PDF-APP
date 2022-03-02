<template>
  <div class="header d-flex justify-content-between">
    <div class="logo">
      <img src="@/assets/pdf.svg" alt="" />
    </div>
    <div class="colu">
      <div class="btn-choose" v-if="!loading">
        <input
          type="file"
          id="file"
          multiple
          required
          @change="UploadFiles"
          accept=".pdf,.doc"
          ref="pdfs"
        />
        <label for="file" class="btn-3">
          <span>Choose PDF Files</span>
        </label>
      </div>
      <div class="btn-choose" v-else>
        <button type="submit" class="btn-send" disabled>
          <div class="spinner-border" role="status">
            <span class="visually-hidden">Loading...</span>
          </div>
        </button>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      company_name: "",
      pdfs: [],
      url: "https://pdf.smarttechno.co/api/pdf",
      loading: false,
    };
  },
  methods: {
    async UploadFiles(event) {
      this.pdfs = event.target.files;
      this.loading = true;
      const formData = new FormData();
      for (var i = 0; i < this.$refs.pdfs.files.length; i++) {
        let file = this.$refs.pdfs.files[i];
        formData.append("company", this.company_name);
        formData.append("pdfs[" + i + "]", file);
      }
      const headers = { "Content-Type": "multipart/form-data" };
      axios
        .post(this.url, formData, { headers })
        .then((res) => {
          this.$store.state.result = res.data;
          this.$emit("change", res.data);
          this.loading = false;
        })
        .catch(console.error);
    },
  },
};
</script>

<style lang="scss">
.header {
  width: 100%;
  height: 60px;
  padding: 10px;
  box-shadow: 0 3px 3px rgba(0, 0, 0, 0.2);
  img {
    width: 60px;
  }
}
.btn-choose {
  .btn-send {
    border: none;
    color: #fff;
    cursor: not-allowed;
    font-weight: 500;
    outline: none;
    width: 200px;
    height: 40px;
    padding: 5px;
    background-color: #4784f5;
  }
}
[type="file"] {
  height: 0;
  overflow: hidden;
  width: 0;
}

[type="file"] + label {
  border: none;
  border-radius: 5px;
  color: #fff;
  cursor: pointer;
  font-weight: 500;
  outline: none;
  padding: 0.5rem 15px;
  width: 200px;
  height: 40px;

  &.btn-3 {
    background-color: #4784f5;
    border-radius: 0;
    overflow: hidden;

    span {
      display: inline-block;
      height: 100%;
      transition: all 0.3s;
      width: 100%;
    }

    &:hover {
      background-color: darken(#6d9aee, 30%);
    }
  }
}
</style>
