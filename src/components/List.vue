<template>
  <div class="list">
    <div class="listheader">
      <p class="list-title">{{ title }}</p>
      <p class="list-counter">total: {{ totalCardInList }}</p>
      <div class="deletelist" @click="removeList">x</div>
    </div>
    <draggable group="cards" :list="cards" @end="$emit('change')">
      <card
        v-for="(item, index) in cards"
        :body="item.body"
        :key="item.id"
        :cardIndex="index"
        :listIndex="listIndex"
      />
    </draggable>
    <card-add :listIndex="listIndex" />
  </div>
</template>

<script>
import draggable from "vuedraggable";
import Card from "./Card";
import CardAdd from "./CardAdd";
export default {
  components: {
    draggable,
    Card,
    CardAdd,
  },
  props: {
    title: {
      type: String,
      required: true,
    },
    cards: {
      type: Array,
      required: true,
    },
    listIndex: {
      type: Number,
      required: true,
    },
  },
  computed: {
    totalCardInList() {
      return this.cards.length;
    },
  },
  methods: {
    removeList: function() {
      if (confirm("本当にこのリストを削除しますか？")) {
        this.$store.dispatch("removelist", { listIndex: this.listIndex });
      }
    },
  },
};
</script>
