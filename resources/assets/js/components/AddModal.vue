<template>
  <div class="modal" :class="acticeModal">
    <div class="modal-background"></div>
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">Modal title</p>
        <button class="delete" aria-label="close" @click="closeModal"></button>
      </header>
      <section class="modal-card-body">
        <div class="field">
          <label class="label">Name</label>
          <div class="control">
            <input class="input" type="text" placeholder="Name" v-model="lists.name">
            <span class="has-text-danger" v-if="errors.name"> {{errors.name[0]}} </span>
          </div>
        </div>
        <div class="field">
          <label class="label">Phone</label>
          <div class="control">
            <input class="input" type="text" placeholder="Phone" v-model="lists.phone">
             <span class="has-text-danger" v-if="errors.name"> {{errors.phone[0]}} </span>
          </div>
        </div>
        <div class="field">
          <label class="label">Email</label>
          <div class="control">
            <input class="input" type="text" placeholder="Email" v-model="lists.email">
             <span class="has-text-danger" v-if="errors.name"> {{errors.email[0]}} </span>
          </div>
        </div>
       
      </section>
      <footer class="modal-card-foot">
        <button class="button is-success" @click="save">Save </button>
        <button class="button" @click="closeModal">Cancel</button>
      </footer>
    </div>
  </div>

</template>

<script>
export default {
  props: ["acticeModal"],
  data() {
    return {
      lists: {
        name: "",
        phone: "",
        email: ""
      },
      errors: {}
    };
  },
  methods: {
    closeModal() {
      this.$emit("closeModal");
    },
    save() {
      axios
        .post("http://localhost/bifumes-pp/public/phonebook", this.$data.lists)
        .then(res => {
          console.log(res.data);
          this.$parent.lists.push(res.data);
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>
