<template>
  <div class="">
    <div class="accordion" id="accordionExample">
      <div
        class="accordion-item"
        v-for="(content, title, indx) in result"
        :key="indx"
      >
        <h2
          class="accordion-header"
          :id="`heading${title.slice(0, 3).trim()}${indx}`"
        >
          <button
            class="accordion-button"
            type="button"
            data-bs-toggle="collapse"
            :data-bs-target="`#collapse${title.slice(0, 3).trim()}${indx}`"
            aria-expanded="true"
            :aria-controls="`collapse${title.slice(0, 3).trim()}${indx}`"
          >
            <span>{{ title }}</span>
          </button>
          <span class="add" @click="addKeys">+</span>
        </h2>
        <div
          :id="`collapse${title.slice(0, 3).trim()}${indx}`"
          class="accordion-collapse collapse"
          :aria-labelledby="`heading${title.slice(0, 3).trim()}${indx}`"
          data-bs-parent="#accordionExample"
        >
          <div class="accordion-body">
            {{ content }}
          </div>
        </div>
      </div>
    </div>
    <div class="list" v-if="keys.length != 0">
      <button class="btn btn-primary" @click="createTable">
        Add To Comparison
      </button>
      <ul class="list-group">
        <li class="list-group-item" v-for="(key, i) in keys" :key="i">
          <div class="d-flex justify-content-between align-items-center">
            <span>{{ key }}</span>
            <span class="delete" @click="deleteElement($event)">&times;</span>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
// import draggable from "vuedraggable";

export default {
  name: "App",
  // components: {
  //   draggable,
  // },
  props: ["result"],
  data() {
    return {
      files: [],
      keys: [],
      vals: [],
      process: true,
    };
  },
  mounted() {
    this.files.push(this.result);
  },
  methods: {
    addKeys(ev) {
      let myElement = ev.target.parentElement.parentElement;
      let title = myElement.children[0].innerText.slice(0, -1).trim();
      let content = myElement.children[1].innerText.trim();
      if (!this.keys.includes(title)) {
        this.keys.push(title);
        this.vals.push(content);
      } else {
        return 0;
      }
    },
    insertHeads(place) {
      // cont.className = "col";
      if (place.children.length == 0) {
        this.keys.forEach((ele) => {
          let cont = document.createElement("tr");
          let head = document.createElement("th");
          let idx = this.keys.findIndex((el) => el == ele);
          head.innerHTML = ele;
          cont.appendChild(head);
          this.insertData(cont, idx);
          place.appendChild(cont);
          // head.className = "row";
          // let tit = document.createElement("span");
          // tit.className = "col-3 col-lg-2 col-md-3 col-sm-3 headTitle";
          // let con = document.createElement("span");
          // con.className = "col-9 col-lg-10 col-md-9 col-sm-9 headContent";
          // con.innerHTML = this.vals[el_idx];
          // head.appendChild(tit);
          // head.appendChild(con);
        });
      } else {
        let cont = document.querySelectorAll(".tableC tr");
        cont.forEach((tr, i) => {
          this.insertData(tr, i);
        });
      }
    },
    insertData(row, idx) {
      let head = document.createElement("td");
      head.innerHTML = this.vals[idx];
      row.appendChild(head);
      // this.vals.forEach((ele) => {
      // let tit = document.createElement("span");
      // tit.className = "col-9 col-lg-10 col-md-9 col-sm-9 headContent";
      // });
    },
    createTable() {
      let cont = document.querySelector(".tableC");
      this.insertHeads(cont);
      // cont
      //   .querySelectorAll(".col:not(:first-child) .row .headTitle")
      //   .forEach((titl) => {
      //     titl.remove();
      //   });
    },
    deleteElement(ev) {
      let ele = ev.target.parentElement.innerText.slice(0, -1).trim();
      let el_idx = this.keys.findIndex((el) => el == ele);
      this.keys.splice(el_idx, 1);
      this.vals.splice(el_idx, 1);
    },
  },
};
</script>
<style scoped>
.delete {
  font-size: 1.5rem;
  cursor: pointer;
}
tr:nth-child(even) {
  background-color: #d6eeee;
}
.accordion-header {
  display: flex;
}
.add {
  height: 52px;
  max-height: 52px;
  z-index: 999;
  padding: 5px 10px;
  cursor: pointer;
}
.add:hover {
  color: rgb(15, 97, 7);
}
.accordion {
  width: 75%;
  float: left;
}
.list {
  width: 25%;
  float: left;
}
.accordion-button:not(.collapsed) {
  background: transparent;
}
.accordion-button:focus {
  border-color: transparent;
  box-shadow: transparent;
}
.accordion-button:not(.collapsed)::after {
  background-image: none;
}
.accordion-button::after {
  background-image: none;
}
</style>
