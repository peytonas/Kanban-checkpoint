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

.delete-button {
  display: inline-block;
  padding: 3px 8px;
  font-size: 15px;
  text-align: center;
  outline: none;
  color: #fff;
  background-color: #4f43ae;
  border: none;
  border-radius: 15px;
  box-shadow: 0 5px #312879;
}
.delete-button:hover {
  background-color: #3f3494;
}
.delete-button:active {
  background-color: #4f43ae;
  box-shadow: 0 3px #312879;
  transform: translateY(4px);
}
.delete-button:focus {
  outline: 0;
}
</style>