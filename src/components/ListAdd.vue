<template>

<form :class="classList" @submit.prevent="addList">
  <input v-model="title"
          type="text"
          class="text-input"
          placeholder="Add new list"
          @focusin="startEditing"
          @focusout="finishEditing"
  >
<button type="submit"
        class="add-button"
        v-if="isEditing || titleExists">
  Add
</button>
</form>

</template>

<script>
export default {
  data: function() {
    return {
      title: '',
      isEditing: false,
    }
  },
  // ★ここから追記
  methods: {
    addList: function() {
      this.$store.dispatch('addlist', { title: this.title })
      this.title = ''
    },
    startEditing() {
      this.isEditing = true
    },
    finishEditing() {
      this.isEditing = false
    },
  },
  computed: {
    classList() {
      const classList = ['addlist']

      if (this.isEditing) {
        classList.push('active')
      }
      // ★ここから追記
      if (this.titleExists) {
        classList.push('addable')
      }
      // ★ここまで追記
      return classList
    },
    // ★ここから追記
    titleExists() {
      return this.title.length > 0
    },
    // ★ここまで追記
  }
}
</script>