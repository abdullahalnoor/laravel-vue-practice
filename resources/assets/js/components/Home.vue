<template>
<div>
    <nav class="panel">
  <p class="panel-heading">
    Phone book 
     <a href="" class="button is-success" @click.prevent="openModal">
       <i class="fa fa-plus"> </i>
       Add
     </a>
     <span v-if="loading">
       loading...
     </span>
  </p>
  <div class="panel-block">
    <p class="control has-icons-left">
      <input class="input is-small" type="text" placeholder="search" v-model="seatchQuery">
      <span class="icon is-small is-left">
        <i class="fas fa-search" aria-hidden="true"></i>
      </span>
    </p>
  </div>
  <p class="panel-tabs">
    <a class="is-active">all</a>
    <a>public</a>
    <a>private</a>
    <a>sources</a>
    <a>forks</a>
  </p>
  <a class="panel-block is-active" v-for="(item,index) in temp" :key="index">
    {{item.name}}
  <span @click="openViewModal(index)" >View</span>
  <span @click="editModal(index)">Edit</span>
  <span @click="del(index,item.id)">Delete</span>
  </a>
 
 
 
</nav>
<add-modal :acticeModal="AddModactive" @closeModal="closeModal"></add-modal>
<view-modal :vuewModal="ViewModactive" @closeModal="closeModal"></view-modal>
<edit-modal :editModal="EditModactive" @closeModal="closeModal"></edit-modal>


</div>
</template>

<script>
const AddModal = require("./AddModal.vue");
const ViewModal = require("./ViewModal.vue");
const EditModal = require("./EditModal");

export default {
  components: {
    AddModal,
    ViewModal,
    EditModal
  },
  data() {
    return {
      AddModactive: "",
      ViewModactive: "",
      EditModactive: "",
      lists: {},
      loading: false,
      seatchQuery: "",
      temp: ""
    };
  },
  created() {
    axios.get("http://localhost/bifumes-pp/public/getData").then(res => {
      this.lists = this.temp = res.data;
      // console.log(res.data);
    });
  },
  watch: {
    seatchQuery() {
      if (this.seatchQuery.length > 0) {
        console.log(this.seatchQuery);
        // let result
        this.temp = this.lists.filter(item => {
          // console.log(item);

          let ab =
            item.name.toLowerCase().indexOf(this.seatchQuery.toLowerCase()) >
            -1;
          // console.log(ab);
          return ab;
        });
        // console.log(result);
      } else {
        this.temp = this.lists;
      }
    }
  },
  methods: {
    // modal part
    openModal() {
      this.AddModactive = "is-active";
    },
    openViewModal(index) {
      this.ViewModactive = "is-active";
      this.$children[1].list = this.lists[index];
      console.log(this.$children);
    },
    editModal(index) {
      this.EditModactive = "is-active";
      this.$children[2].list = this.lists[index];
    },
    del(index, id) {
      this.loading = true;
      // console.log(`${index}, ${id}`);
      if (confirm("Are Youe Sure ?")) {
        axios
          .delete(`http://localhost/bifumes-pp/public/phonebook/${id}`)
          .then(res => {
            // console.log("delete");
            this.lists.splice(index, 1);
            this.loading = false;
          });
      }
    },
    closeModal() {
      this.AddModactive = this.ViewModactive = this.EditModactive = "";
    }
  }
};
</script>

