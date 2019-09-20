<template>
  <div class="col-3 card card-background font ml-2">
    <div class="card-body text-color">
      <h5 class="card-title">{{listProp.title}}</h5>
      <!-- start of card in card -->
      <div class="row justify-content-center">
        <div class="col-3 mt-1">
          <div class="row justify-content-center">
            <button
              class="nes-btn is-success"
              data-toggle="modal"
              :data-target="'#create-task-modal' +listProp._id"
            >Create A Task</button>
          </div>
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
  background-color: #4f43ae;
}
</style>