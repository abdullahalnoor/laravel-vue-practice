<template>
  <div>
    <div class="modal" :class="vuewModal">
  <div class="modal-background"></div>
  <div class="modal-card">
    <header class="modal-card-head">
      <p class="modal-card-title">Modal title</p>
      <button class="delete" aria-label="close" @click="closeModal"></button>
    </header>
    <section class="modal-card-body">
     <ul>
       <li> {{list.name}} </li>
       <li> {{list.phone}} </li>
       <li> {{list.email}} </li>
     </ul>
    </section>
    <footer class="modal-card-foot">
      <button class="button"  @click="closeModal">Cancel</button>
    </footer>
  </div>
</div>
  </div>
</template>
<script>
export default {
  props: ["vuewModal"],
  data() {
    return {
      list: {}
    };
  },
  methods: {
    closeModal() {
      this.$emit("closeModal");
    }
  }
};
</script>

