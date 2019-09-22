<template>
  <div id="create-list-modal" class="modal" tabindex="-1" role="dialog">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title text-color">Create A List!</h5>
          <button class="nes-btn is-error" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <form @submit.prevent="addList()">
            <div class="form-group text-color">
              <label for="title">Title</label>
              <input
                type="text"
                class="form-control"
                id="title"
                placeholder="Enter a title..."
                v-model="newList.title"
                required
              />
            </div>
            <button type="submit" class="nes-btn is-success">Make List</button>
          </form>
        </div>
        <div class="modal-footer"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "create-list-modal",
  props: ["boardId"],
  data() {
    return {
      newList: {}
    };
  },
  methods: {
    addList() {
      this.newList.boardId = this.$route.params.boardId; //route=URL, look in params of URl and get boardId;
      this.$store.dispatch("addList", this.newList);
      this.newList = {};
    }
  },
  computed: {},
  components: {}
};
</script>


<style scoped>
.text-color {
  color: #908a99;
}
</style>