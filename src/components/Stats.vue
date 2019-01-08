<template>
    <div class="stats">
        <h1>This is another Component </h1>
        <p> Number of Links: {{countLinks}} </p>
        <button @click="removeAllLinks">Remove All Links</button>
        <p v-if="showCounter">All links will be removed in {{counter}} seconds.</p>
        <p v-if="showMessage">{{msg}}</p>

    </div>
</template>

<script>
import { mapGetters, mapMutations, mapActions } from "vuex";

export default {
  name: "Stats",
  data() {
    return {
      msg: "",
      counter: "5",
      showCounter: false
    };
  },
  computed: {
    ...mapGetters(["countLinks"]),
    showMessage: function() {
      if (this.countLinks > 0) {
        return false;
      } else {
        return true;
      }
    }
  },
  methods: {
    ...mapMutations(["REMOVE_ALL"]),
    ...mapActions(["removeAll"]),
    removeAllLinks: function() {
      this.showCounter = true;
      var interval = setInterval(() => {
        this.counter--;
      }, 1000);
      this.removeAll().then(() => {
        this.msg = "All Links have been removed";
        this.showCounter = !this.showCounter;
        this.counter = 5;
        clearInterval(interval);
      });
    }
  }
};
</script>

<style>
button {
  width: 100%;
  padding: 10px;
  background: none;
  outline: 0;
  cursor: pointer;
  border: 1px solid lightgray;
}
</style>
