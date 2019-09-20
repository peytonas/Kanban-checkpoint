<template>
  <div class="col-4 card card-background font">
    <div class="card-body text-color">
      <h5 class="card-title">{{listProp.title}}</h5>
      <!-- start of card in card -->
      <div class="row justify-content-center">
        <div class="col-3 mt-1">
          <button
            class="nes-btn"
            data-toggle="modal"
            :data-target="'#create-task-modal' +listProp._id"
          >Create A Task</button>
        </div>
      </div>
      <TaskModal :listId="listProp._id" />
      <div class="col-12 mt-3">
        <task v-for="task in tasks" :taskProp="task" :key="task._id" />
      </div>
      <!-- end of card in card -->
    </div>
    <div class="row justify-content-center">
      <button class="nes-btn is-error" @click.prevent="deleteList()">
        <i class="nes-icon close is-small"></i>
      </button>
    </div>
  </div>
</template>

<script>
import task from "../components/Task";
import TaskModal from "../components/TaskModal";
export default {
  name: "List",
  mounted() {
    this.$store.dispatch("getTasks", this.listProp._id);
  },
  props: ["listProp"],
  methods: {
    deleteList() {
      this.$store.dispatch("deleteList", this.listProp);
    }
  },
  data() {
    return {};
  },
  computed: {
    tasks() {
      return this.$store.state.tasks[this.listProp._id]; //filter through array of tasks, show only the ones by listId
    }
  },
  components: { task, TaskModal }
};
</script>

<style scoped>
.text-color {
  color: #908a99;
}
.font {
  font-family: "Press Start 2p";
  font-size: 5px;
}
.card-background {
  background-color: #211a21;
}
.task-button {
  display: inline-block;
  padding: 3px 8px;
  font-size: 12px;
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
  font-size: 10px;
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