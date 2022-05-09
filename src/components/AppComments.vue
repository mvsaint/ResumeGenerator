<template>
  <p v-if="isShowBtn">
    <button class="btn primary" @click="load">Загрузить комментарии</button>
  </p>
  <div class="card" v-if="comments.length">
    <h2>Комментарии</h2>
    <ul class="list">
      <li class="list-item" v-for="item in comments" :key="item.id">
        <div>
          <p><strong>{{ item.email }}</strong></p>
          <small>{{ item.body }}</small>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'AppComments',
  emits: ['loadComments'],
  props: ['comments'],
  data() {
    return {
      isShowBtn: true
    }
  },
  methods: {
    load() {
      this.$emit('loadComments')
      this.isShowBtn = false
    }
  }
}
</script>

<style scoped>

</style>
