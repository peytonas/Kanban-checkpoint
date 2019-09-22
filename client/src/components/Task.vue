<template>
  <div class="container">
    <div>
      <h5 class="text-color">{{taskProp.title}}</h5>
    </div>
    <button class="nes-btn is-error" @click.prevent="deleteTask()">
      <i class="nes-icon close is-small"></i>
    </button>
    <!-- comment card in card -->
    <div class="col-12 mt-3">
      <button
        class="nes-btn is-success"
        data-toggle="modal"
        :data-target="'#create-comment-modal' + taskProp._id"
      >Add a comment</button>
    </div>
    <commentModal :taskId="taskProp._id" :listId="taskProp.listId" />
    <div class="col-12 mt-3">
      <comment class="mt-2" v-for="comment in comments" :commentProp="comment" :key="comment._id" />
    </div>
    <!-- end of comment card -->
    <!-- dropdown for list select -->
    <div class="nes-select font text-color">
      <select v-model="selected">
        <option value disabled selected hidden>Move task...</option>
        <option v-for="list in lists" :key="list._id" :value="list._id">{{list.title}}</option>
      </select>
    </div>
    <button class="nes-btn is-warning" @click="moveTask()">Move it</button>
    <!-- </div> -->
  </div>
</template>

<script>
import comment from "../components/Comment";
import commentModal from "../components/CommentModal";
export default {
  name: "Task",
  props: ["taskProp"],
  mounted() {
    this.$store.dispatch("getComments", this.taskProp._id);
  },
  data() {
    return {
      selected: ""
    };
  },
  methods: {
    data() {
      return {};
    },
    deleteTask() {
      this.$store.dispatch("deleteTask", this.taskProp);
    },
    moveTask() {
      this.$store.dispatch("moveTask", {
        taskId: this.taskProp._id,
        listId: this.selected,
        oldListId: this.taskProp.listId
      });
    }
  },
  computed: {
    comments() {
      return this.$store.state.comments[this.taskProp._id]; //filter through array of tasks, show only the ones by listId
    },
    lists() {
      return this.$store.state.lists;
    }
  },
  components: { comment, commentModal }
};
</script>

<style scoped>
.text-color {
  color: #908a99;
}
.font {
  font-family: "Press Start 2p";
  font-size: 10px;
}
</style>
