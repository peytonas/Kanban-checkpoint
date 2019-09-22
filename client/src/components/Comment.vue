<template>
  <div class="card">
    <div class="card-body text-color">
      <p class="card-text">{{commentProp.body}}</p>
    </div>
    <div class="row justify-content-center">
      <button class="nes-btn is-error" @click.prevent="deleteComment()">
        <i class="nes-icon close is-small"></i>
      </button>
    </div>
  </div>
</template>


<script>
export default {
  name: "Comment",
  props: ["commentProp"],
  data() {
    return {};
  },
  computed: {},
  methods: {
    deleteComment() {
      this.$store.dispatch("deleteComment", this.commentProp);
    }
  },
  components: {}
};
</script>


<style scoped>
.text-color {
  color: #908a99;
}
</style>