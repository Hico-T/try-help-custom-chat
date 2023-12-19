<template>
  <div class="sc-suggestions-row" :style="{background: colors.messageList.bg}">
    <div
      v-for="(suggestion, idx) in suggestions"
      :key="idx"
      class="sc-suggestions-element"
      @click="$emit('sendSuggestion', suggestion)"
    >
      {{ suggestion }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    suggestions: {
      type: Array,
      default: () => []
    },
    colors: {
      type: Object,
      required: true
    }
  },
  data() {
    return {}
  }
}
</script>

<style>
.sc-suggestions-row {
  text-align: right;
  background: inherit;
    margin-right: 10px;
    width: calc(100% - 30px);
    margin-left: 15px;
    margin-bottom: 10px;
}

.sc-suggestions-element:hover {
  background: #CBE9FF;
  /* color: #fff; */
}
.sc-suggestions-element {
      max-width: calc(100% - 15px);
    border-radius: 12px 0px 12px 12px;
    background-color: #E7F4FE;
    padding: 7px;
    text-align: center;
    color: #333;
    overflow: hidden;
    transition: all .5s ease;
    margin-top: 10px;
    font-weight: 400;
    cursor: pointer;
    font-size: 14px;
}

@media (min-width: 761px) {
  .sc-suggestions-row{
  max-width: calc(100% - 15px);
  }
}
</style>
