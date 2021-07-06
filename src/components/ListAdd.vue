<template>
  <form :class="classList" @submit.prevent="addList">
    <input
      v-model="title"
      type="text"
      class="text-input"
      placeholder="リストを追加"
      @focusin="startEditing"
      @focusout="finishEditing"
    />
    <button type="submit" class="add-button" v-if="isEditing || titleExists">
      Add
    </button>
  </form>
</template>

<script>
export default {
  data: function() {
    return {
      title: "",
      isEditing: false,
    };
  },
  computed: {
    //computedはdataの状態を監視できる
    titleExists() {
      return this.title.length > 0;
    },
    classList() {
      //trueであればクラスを追加
      const classList = ["addlist"];
      if (this.isEditing) {
        classList.push("active");
      }
      if (this.titleExists) {
        classList.push("addable");
      }
      return classList;
    },
  },
  methods: {
    addList: function() {
      this.$store.dispatch("addlist", { title: this.title });
      this.title = "";
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
