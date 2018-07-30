<template>
  <div>


    <div class="modal" :class="editModal">
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
              <input class="input" type="text" v-model="list.name">
            </div>
          </div>
          <div class="field">
            <label class="label">phone</label>
            <div class="control">
              <input class="input" type="text" v-model="list.phone">
            </div>
          </div>
          <div class="field">
            <label class="label">email</label>
            <div class="control">
              <input class="input" type="text" v-model="list.email">
            </div>
          </div>

        </section>
        <footer class="modal-card-foot">
          <button class="button is-success" @click="update">update </button>
          <button class="button" @click="closeModal">Cancel</button>
        </footer>
      </div>
    </div>

  </div>
</template>
<script>
export default {
  props: ["editModal"],
  data() {
    return {
      list: {}
    };
  },
  methods: {
    closeModal() {
      this.$emit("closeModal");
    },
    update() {
      axios
        .patch(
          `http://localhost/bifumes-pp/public/phonebook/${this.list.id}`,
          this.$data.list
        )
        .then(res => {
          console.log(res.data);
        });
    }
  }
};
</script>
