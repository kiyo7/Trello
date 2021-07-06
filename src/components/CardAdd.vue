<template>
  <form :class="classList" @submit.prevent="addCardToList">
    <input
      v-model="body"
      type="text"
      class="text-input"
      placeholder="カードを追加"
      @focusin="startEditing"
      @focusout="finishEditing"
    />
    <button type="submit" class="add-button" v-if="bodyExists || isEditing">
      追加する
    </button>
  </form>
</template>
<script>
export default {
  props: {
    listIndex: {
      type: Number,
      required: true,
    },
  },
  data: function() {
    return {
      body: "",
      isEditing: false,
    };
  },
  computed: {
    bodyExists() {
      return this.body.length > 0;
    },
    classList() {
      const classList = ["addcard"];
      if (this.isEditing) {
        classList.push("active");
      }
      if (this.bodyExists) {
        classList.push("addable");
      }
      return classList;
    },
  },
  methods: {
    addCardToList: function() {
      this.$store.dispatch("addCardToList", {
        body: this.body,
        listIndex: this.listIndex,
      });
      this.body = "";
    },
    startEditing: function() {
      this.isEditing = true;
    },
    finishEditing: function() {
      this.isEditing = false;
    },
  },
};
</script>
