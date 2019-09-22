<template>
  <div class="container-fluid font">
    <div class="row justify-content-between">
      <div class="col-1 mt-2">
        <button class="nes-btn is-primary mt-2 text-dark" @click="gotoBoards()">Boards</button>
      </div>
      <div class="col-1 mt-2">
        <button class="nes-btn is-error" @click="deleteBoard()">
          <i class="nes-icon close is-small"></i>
        </button>
      </div>
    </div>
    <div class="row justify-content-center">
      <div class="col-6 justify-space-between">
        <h1 class="nes-container is-rounded is-centered font">
          <h1 class="text-color">{{board.title}}</h1>
        </h1>
      </div>
    </div>
    <div class="row justify-space-between">
      <div class="col-12 mt-3">
        <button
          class="nes-btn is-success mb-2"
          data-toggle="modal"
          data-target="#create-list-modal"
        >Create A List</button>
      </div>
      <ListModal :boardId="$route.params.boardId" />
    </div>
    <div class="row justify-content-around">
      <list class="mt-2" v-for="list in lists" :listProp="list" :key="list._id" />
    </div>
  </div>
</template>

<script>
import list from "../components/List";
import ListModal from "../components/ListModal";

export default {
  name: "board",
  mounted() {
    this.$store.dispatch("getLists", this.boardId); //which board has the lists
    this.$store.dispatch("getBoards");
  },
  computed: {
    board() {
      return (
        //FIXME This does not work on page reload because the boards array is empty in the store
        this.$store.state.boards.find(b => b._id == this.boardId) || {
          title: "Loading..."
        }
      );
    },
    lists() {
      return this.$store.state.lists;
    }
  },
  methods: {
    deleteBoard() {
      this.$store.dispatch("deleteBoard", this.boardId);
    },
    gotoBoards() {
      this.$router.push("/boards");
    }
  },
  props: ["boardId"],
  components: { list, ListModal }
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
