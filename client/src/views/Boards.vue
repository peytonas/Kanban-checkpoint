<template>
  <div class="container-fluid font">
    <div class="row justify-content-end">
      <div class="col-1 mt-2">
        <button class="nes-btn is-error text-white" @click="logout()">
          <i class="nes-icon close is-small"></i>
        </button>
      </div>
    </div>
    <div class="row justify-content-center">
      <div class="col-6">
        <h1 class="nes-container is-rounded is-centered text-color">
          <p>Welcome home, {{this.$store.state.user.name}}!!!</p>
        </h1>
      </div>
    </div>

    <!-- <section>
            <button
              type="button"
              class="nes-btn is-error"
              onclick="document.getElementById('dialog-dark-rounded').showModal();"
            >logout</button>
            <dialog class="nes-dialog is-dark is-rounded" id="dialog-dark-rounded">
              <form method="dialog">
                <p>Are you sure you want to log out?</p>
                <menu class="dialog-menu">
                  <button class="nes-btn">Cancel</button>
                  <button class="nes-btn is-primary">Confirm</button>
                </menu>
              </form>
            </dialog>
    </section>-->

    <form class="mt-3" @submit.prevent="addBoard()">
      <input
        type="text"
        placeholder="title..."
        class="nes-input col-3 mt-3"
        v-model="newBoard.title"
        required
      />
      <button class="nes-btn ml-2">Create Board</button>
    </form>
    <router-link
      :to="{name: 'board', params: {boardId: board._id}}"
      class="mt-3 ml-2 nes-btn text-dark"
      v-for="board in boards"
      :key="board._id"
    >{{board.title}}</router-link>
  </div>
</template>

<script>
import Auth from "../AuthService";

export default {
  name: "boards",
  mounted() {
    this.$store.dispatch("getBoards"); //which board has the lists
  },
  data() {
    return {
      newBoard: {
        title: ""
      }
    };
  },
  computed: {
    boards() {
      return this.$store.state.boards;
    }
  },
  methods: {
    addBoard() {
      this.$store.dispatch("addBoard", this.newBoard);
      this.newBoard = { title: "" };
    },
    logout() {
      this.$store.dispatch("logout");
    }
  }
};
</script>
<style scoped>
.font {
  font-family: "Press Start 2p";
  font-size: 10px;
}
.text-color {
  color: #908a99;
}
/* .board-button {
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
.board-button:hover {
  background-color: #a4a5d3;
}
.board-button:active {
  background-color: #8d8ebe;
  box-shadow: 0 3px #606188;
  transform: translateY(4px);
} */
.nes-btn:focus {
  outline: 0;
}
/* .logout-button {
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
.logout-button:hover {
  background-color: #3f3494;
}
.logout-button:active {
  background-color: #4f43ae;
  box-shadow: 0 3px #312879;
  transform: translateY(4px);
}
.logout-button:focus {
  outline: 0;
} */
</style>