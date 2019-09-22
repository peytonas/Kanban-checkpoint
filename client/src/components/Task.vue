<template>
  <div class="container">
    <div v-drag-and-drop:options="options">
      <div>
        <h3 class="text-color">{{taskProp.title}}</h3>
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
      </div>
    </div>
    <commentModal :taskId="taskProp._id" :listId="taskProp.listId" />
    <div class="col-12 mt-3">
      <comment class="mt-2" v-for="comment in comments" :commentProp="comment" :key="comment._id" />
    </div>
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
    const componentInstance = this;
    return {
      selected: "",
      options: {
        dropzoneSelector: "drop",
        draggableSelector: "div",
        showDropzoneAreas: true,
        multipleDropzonesItemsDraggingEnabled: true,
        onDrop(event) {
          console.log(event);
        },
        onDragStart(event) {
          event.start();
        },
        onDragEnd(event) {
          event.stop;
        }
      }
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
