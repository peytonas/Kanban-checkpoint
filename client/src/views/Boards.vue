<template>
  <div class="row">
    <div class="col">
      <div>
        <h1 class="text-color">WELCOME TO THE BOARDS!!!</h1>
        <button class="logout-button" @click="logout()">Logout</button>
        <form class="mt-3" @submit.prevent="addBoard()">
          <input type="text" placeholder="title" v-model="newBoard.title" required />
          <input type="text" placeholder="description" v-model="newBoard.description" />
          <button class="board-button">Create Board</button>
        </form>
        <button class="mt-3 board-button" v-for="board in boards" :key="board._id">
          <router-link
            :to="{name: 'board', params: {boardId: board._id}}"
            class="text-white"
          >{{board.title}}</router-link>
        </button>
      </div>
    </div>
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
        title: "",
        description: ""
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
      this.newBoard = { title: "", description: "" };
    },
    logout() {
      this.$store.dispatch("logout");
    }
  }
};
</script>
<style scoped>
.text-color {
  color: #908a99;
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
.logout-button {
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
}
</style>