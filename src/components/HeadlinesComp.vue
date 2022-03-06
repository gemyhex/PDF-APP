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
      <button class="btn btn-primary" @click="createTable">Add To Table</button>
      <ul class="list-group">
        <li class="list-group-item" v-for="(key, i) in keys" :key="i">
          <div class="d-flex justify-content-around align-items-center">
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
    };
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
    insertHeads(table) {
      let row = document.createElement("tr");
      this.keys.forEach((ele) => {
        let heading = document.createElement("th");
        let content = document.createElement("td");
        heading.innerHTML = ele;
        let el_idx = this.keys.findIndex((el) => el == ele);
        content.innerHTML = this.vals[el_idx];
        row.appendChild(heading);
        row.appendChild(content);
        table.appendChild(row);
      });
    },
    // insertData(table) {
    //   let row = document.createElement("tr");
    //   this.vals.forEach((ele) => {
    //     let heading = document.createElement("td");
    //     heading.innerHTML = ele;
    //     row.appendChild(heading);
    //   });
    //   table.appendChild(row);
    // },
    createTable() {
      let table = document.querySelector("table");
      this.insertHeads(table);
      // this.insertData(table);
      document.querySelector(".table").appendChild(table);
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
  width: 20%;
  float: right;
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
