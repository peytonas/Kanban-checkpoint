<template>
  <div class="container-fluid font">
    <div class="row justify-content-between">
      <div class="col-1 mt-2">
        <button class="nes-btn is-primary mt-2 text-dark" @click="gotoBoards()">Boards</button>
      </div>
      <div class="col-1 mt-2">
        <button
          class="nes-btn is-error"
          onclick="document.getElementById('dialog-rounded').showModal();"
        >
          <i class="nes-icon close is-small"></i>
        </button>
        <dialog class="nes-dialog is-rounded" id="dialog-rounded">
          <form method="dialog">
            <p>Are you sure you want to delete this board?</p>
            <menu class="dialog-menu">
              <button class="nes-btn">Cancel</button>
              <button class="nes-btn is-primary" @click="deleteBoard()">Confirm</button>
            </menu>
          </form>
        </dialog>
      </div>
      <!-- <section>
    <button
      type="button"
      class="nes-btn is-primary"
      onclick="document.getElementById('dialog-rounded').showModal();"
    >Open rounded dialog</button>
    <dialog class="nes-dialog is-rounded" id="dialog-rounded">
      <form method="dialog">
        <p class="title">Rounded dialog</p>
        <p>Alert: this is a dialog.</p>
        <menu class="dialog-menu">
          <button class="nes-btn">Cancel</button>
          <button class="nes-btn is-primary">Confirm</button>
        </menu>
      </form>
    </dialog>
      </section>-->
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
    <div class="row">
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
.board-button {
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
.board-button:hover {
  background-color: #a4a5d3;
}
.board-button:active {
  background-color: #8d8ebe;
  box-shadow: 0 3px #606188;
  transform: translateY(4px);
}
.board-button:focus {
  outline: 0;
}
.delete-button {
  display: inline-block;
  padding: 3px 8px;
  font-size: 12px;
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
