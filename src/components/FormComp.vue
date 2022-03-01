<template>
  <form class="form" @submit.prevent="UploadFiles">
    <div class="upload">
      <div class="colu mb-3">
        <input
          type="text"
          class="form-control text-center"
          id="company_name"
          v-model="company_name"
          placeholder="Company Name"
        />
      </div>
      <div class="colu mb-3">
        <input
          type="file"
          id="file"
          multiple
          required
          @change="onFileChange"
          accept=".pdf,.doc"
          ref="pdfs"
        />
        <label for="file" class="btn-3">
          <span>Choose PDF Files</span>
        </label>
      </div>
    </div>
    <div class="colu mb-3 text-center">
      <button type="submit" class="btn btn-primary btn-send">Send</button>
    </div>
  </form>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      company_name: "",
      pdfs: [],
      url: "https://pdf.smarttechno.co/api/pdf",
    };
  },
  methods: {
    onFileChange(event) {
      this.pdfs = event.target.files;
    },
    async UploadFiles() {
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
        })
        .catch(console.error);
    },
  },
};
</script>

<style lang="scss">
.form {
  padding: 10px;

  #company_name {
    width: 100%;
    height: 50px;
    margin: auto;
    border-radius: 0;
  }

  .upload {
    width: 50%;
    // background: #eee;
    margin: 10px auto;
    padding: 10px;
    // box-shadow: 0 7px 5px 0 #4784f577;
  }
  .btn-send {
    width: 50%;
    height: 50px;
    border-radius: 0;
  }
}
.box {
  width: 100%;
  min-height: 10px;
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
  display: inline-block;
  font-size: inherit;
  font-weight: 500;
  margin-bottom: 1rem;
  outline: none;
  padding: 1rem 50px;
  position: relative;
  transition: all 0.3s;
  vertical-align: middle;
  width: 100%;

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

    &::before {
      color: #fff;
      content: "\F296";
      font-size: 130%;
      height: 100%;
      left: 0;
      line-height: 2.6;
      position: absolute;
      top: -180%;
      transition: all 0.3s;
      width: 100%;
    }

    &:hover {
      background-color: darken(#6d9aee, 30%);

      span {
        transform: translateY(300%);
      }

      &::before {
        top: 0;
      }
    }
  }
}
</style>
