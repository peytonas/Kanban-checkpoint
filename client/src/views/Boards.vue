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
    <form class="mt-3" @submit.prevent="addBoard()">
      <input
        type="text"
        placeholder="title..."
        class="nes-input col-3 mt-3"
        v-model="newBoard.title"
        required
      />
      <button class="nes-btn is-success is-success ml-2">Create Board</button>
    </form>
    <router-link
      :to="{name: 'board', params: {boardId: board._id}}"
      class="mt-3 ml-2 nes-btn is-warning text-dark"
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
</style>