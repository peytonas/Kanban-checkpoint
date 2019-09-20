<template>
  <div :id="'create-comment-modal' + taskId" class="modal" tabindex="-1" role="dialog">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Add a task comment</h5>
          <button type="button" class="delete-button" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <form @submit.prevent="addComment(event)">
            <div class="form-group">
              <label for="body">Body</label>
              <input
                type="text"
                class="form-control"
                id="body"
                placeholder="Enter your comment"
                v-model="newComment.body"
                required
              />
            </div>
            <button type="submit" class="comment-button">Create Comment</button>
          </form>
        </div>
        <div class="modal-footer"></div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: "create-comment-modal",
  props: ["taskId", "listId"],
  data() {
    return {
      newComment: {
        body: "",
        taskId: this.taskId,
        listId: this.listId,
        boardId: this.$route.params.boardId
      }
    };
  },
  computed: {},
  methods: {
    addComment(e) {
      this.$store.dispatch("addComment", this.newComment);
      e.target.reset();
    }
  },
  components: {}
};
</script>


<style scoped>
.text-color {
  color: #908a99;
}
.comment-button {
  display: inline-block;
  padding: 3px 8px;
  font-size: 15px;
  text-align: center;
  outline: none;
  color: #fff;
  background-color: #b5b6e4;
  border: none;
  border-radius: 15px;
  box-shadow: 0 5px #606188;
}
.comment-button:hover {
  background-color: #a4a5d3;
}
.comment-button:active {
  background-color: #8d8ebe;
  box-shadow: 0 3px #606188;
  transform: translateY(4px);
}
.comment-button:focus {
  outline: 0;
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