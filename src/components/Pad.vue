<template>
  <div class="pad">
    <input
      type="text"
      class="pad-title"
      placeholder="Untitled note"
      v-model="note.title"
      v-on:keydown="save"
    />
    <textarea
      class="pad-text"
      placeholder="Start writing..."
      v-model="note.body"
      v-on:keydown="save"
    ></textarea>
    <footer class="pad-footer">
      <ul class="pad-footer-items">
        <li class="pad-footer-item">Words: {{ wordCount }}</li>
        <li class="pad-footer-item pad-footer-item--right">
          Last saved: {{ lastSaved }}
        </li>
      </ul>
    </footer>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
export default {
  computed: {
    ...mapGetters(["note", "lastSaved", "wordCount"])
  },
  methods: {
    ...mapActions(["saveNote", "startSaveTimeout"]),
    save() {
      if (!this.note.id) {
        this.saveNote();
        return;
      }
      this.startSaveTimeout();
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/style/placeholders";
.pad {
  flex: 4;
  display: flex;
  flex-direction: column;
  .pad-title {
    max-width: 100%;
    border: 0;
    font: inherit;
    font-size: 1.6em;
    outline: none;
    padding: 20px;
    padding-left: 30px;
    padding-top: 25px;
  }
  .pad-text {
    flex: 1;
    max-width: 100%;
    margin: 0;
    padding: 20px 30px;
    border: 0;
    font: inherit;
    outline: none;
    resize: none;
    line-height: 2;
    -webkit-mask-image: linear-gradient(
      to bottom,
      transparent 0%,
      #fff 5%,
      #fff 95%,
      transparent 100%
    );
  }

  .pad-footer {
    padding: 20px 30px;
    .pad-footer-items {
      @extend %inline-list;
      .pad-footer-item {
        flex: 1;
        font-size: 0.9em;
      }
      .pad-footer-item--right {
        margin-left: auto;
        text-align: right;
      }
    }
  }
}
</style>
