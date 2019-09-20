<template>
  <div id="create-list-modal" class="modal" tabindex="-1" role="dialog">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title text-color">Create A List!</h5>
          <button class="nes-btn is-error" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <form @submit.prevent="addList()">
            <div class="form-group text-color">
              <label for="title">Title</label>
              <input
                type="text"
                class="form-control"
                id="title"
                placeholder="Enter a title..."
                v-model="newList.title"
                required
              />
            </div>
            <button type="submit" class="nes-btn is-success">Make List</button>
          </form>
        </div>
        <div class="modal-footer"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "create-list-modal",
  props: ["boardId"],
  data() {
    return {
      newList: {}
    };
  },
  methods: {
    addList() {
      this.newList.boardId = this.$route.params.boardId; //route=URL, look in params of URl and get boardId;
      this.$store.dispatch("addList", this.newList);
      this.newList = {};
    }
  },
  computed: {},
  components: {}
};
</script>


<style scoped>
.text-color {
  color: #908a99;
}
.list-button {
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
.list-button:hover {
  background-color: #a4a5d3;
}
.list-button:active {
  background-color: #8d8ebe;
  box-shadow: 0 3px #606188;
  transform: translateY(4px);
}
.list-button:focus {
  outline: 0;
}
.close-button {
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
.close-button:hover {
  background-color: #3f3494;
}
.close-button:active {
  background-color: #4f43ae;
  box-shadow: 0 3px #312879;
  transform: translateY(4px);
}
.close-button:focus {
  outline: 0;
}
</style>