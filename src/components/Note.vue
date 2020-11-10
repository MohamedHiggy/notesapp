<template>
  <div class="note">
    <a href="#" class="note-delete" @click.prevent="deleteNote(note.id)">
      <span class="note-delete-icon">&times;</span>
    </a>
    <div class="note-content">
      <a href="#" class="note-title" @click.prevent="openNote(note)">
        <span v-if="note.title">{{ note.title }}</span>
        <span v-else>Untitled note</span>
      </a>
      <p class="note-body">
        <span v-if="note.body">{{ note.body }}</span>
        <span v-else><em>Empty</em></span>
      </p>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";
export default {
  props: ["note"],
  methods: {
    ...mapActions(["openNote", "deleteNote"])
  }
};
</script>

<style lang="scss" scoped>
.note {
  display: flex;
  color: inherit;
  text-decoration: none;
  border-bottom: 2px dashed #eee;
  opacity: 0.3;
  flex-direction: row;
  max-width: 100%;
  &:hover {
    opacity: 1;
    .note-delete {
      margin-left: 0;
    }
  }
  .note-delete {
    position: relative;
    margin-left: -50px;
    width: 50px;
    display: block;
    background: #cc4466;
    min-height: 100%;
    color: #fff;
    transition: margin-left 100ms ease-in-out;
    .note-delete-icon {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 1.5em;
      font-weight: 600;
    }
  }
  .note-content {
    padding: 30px;
    flex: 2;
    overflow: hidden;
    .note-title {
      display: block;
      font-size: 1em;
      margin: 0;
      font-weight: 500;
      text-decoration: none;
      color: inherit;
      white-space: nowrap;
      &:hover {
        text-decoration: underline;
      }
    }
    .note-body {
      font-size: 0.9em;
      margin-bottom: 0;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
  }
}
</style>
