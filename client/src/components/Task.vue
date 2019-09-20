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
        class="comment-button"
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
        <option value disabled selected hidden>Move selected...</option>
        <option v-for="list in lists" :key="list._id" :value="list._id">{{list.title}}</option>
      </select>
    </div>
    <button class="comment-button" @click="moveTask()">Move it</button>
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
.card-background {
  background-color: #cec9cc;
}
.comment-button {
  display: inline-block;
  padding: 3px 8px;
  font-size: 10px;
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
