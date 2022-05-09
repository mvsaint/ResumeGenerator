<template>
  <form class="card card-w30" @submit.prevent="formSubmit">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" v-model="typeChecked">
        <option
          v-for="type in typeBlocks"
          :key="type.value"
          :value="type.value"
        >{{ type.text }}</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea id="value" rows="3" v-model="value"></textarea>
    </div>

    <button class="btn primary" :disabled="changeValue">Добавить</button>
  </form>
</template>

<script>
export default {
  name: 'AppForm',
  emits: ['formSubmit'],
  data() {
    return {
      typeChecked: 'title',
      typeBlocks: [
        {value: 'title', text: 'Заголовок'},
        {value: 'subtitle', text: 'Подзаголовок'},
        {value: 'avatar', text: 'Аватар'},
        {value: 'text', text: 'Текст'},
      ],
      value: '',
      btnStatus: true
    }
  },
  methods: {
    formSubmit() {
      this.$emit('formSubmit', this.typeChecked, this.value)
      this.typeChecked = 'title',
      this.value = ''
    },
  },
  computed: {
    changeValue() {
      return !(this.value.length > 3)
    }    
  }
}
</script>

<style scoped>

</style>