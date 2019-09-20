<template>
  <div :id="'create-task-modal' + listId" class="modal" tabindex="-1" role="dialog">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Create a task for your list!</h5>
          <button
            type="button"
            class="delete-button text-color"
            data-dismiss="modal"
            aria-label="Close"
          >
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <form @submit.prevent="addTask(event)">
            <div class="form-group">
              <label for="title">Title</label>
              <input
                type="text"
                class="form-control text-color"
                id="title"
                placeholder="Enter a task title"
                v-model="newTask.title"
                required
              />
            </div>
            <button type="submit" class="task-button text-color">Make a Task</button>
          </form>
        </div>
        <div class="modal-footer"></div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: "create-task-modal",
  props: ["listId"],
  data() {
    return {
      newTask: {
        title: "",
        listId: this.listId,
        boardId: this.$route.params.boardId
      }
    };
  },
  methods: {
    addTask(e) {
      this.$store.dispatch("addTask", this.newTask);
      e.target.reset();
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
.task-button {
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
.task-button:hover {
  background-color: #a4a5d3;
}
.task-button:active {
  background-color: #8d8ebe;
  box-shadow: 0 3px #606188;
  transform: translateY(4px);
}
.task-button:focus {
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