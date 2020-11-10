<template>
  <div class="sidebar">
    <div v-if="notes.length">
      <Note v-for="(note, index) in notes" :key="index" :note="note"></Note>
    </div>
    <div v-else class="sidebar-content">
      Boo, no notes. Get writing!
    </div>
    <div class="sidebar-content">
      <a href="#" @click.prevent="clearCurrentNote">Start a new note</a>
    </div>
  </div>
</template>

<script>
import Note from "./Note";
import { mapGetters, mapActions } from "vuex";
export default {
  components: {
    Note
  },
  computed: {
    ...mapGetters(["notes"])
  },
  methods: {
    ...mapActions(["clearCurrentNote"])
  }
};
</script>

<style lang="scss" scoped>
.sidebar {
  background-color: #f9f9f9;
  flex: 1;
  height: 100%;
  max-width: 30%;
  border-right: 2px solid #eee;
  overflow-y: scroll;
  .sidebar-content {
    padding: 30px;
    a {
      text-decoration: none;
      color: inherit;
    }
  }
}
</style>
