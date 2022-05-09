<template>
  <div class="card card-w70">
    <component
      v-for="(item, idx) in blocks"
      :is="'resume-' + item.type"
      :key="idx"
      :value="item.value"
    ></component>
    <h3 v-if="!blocks.length">Добавьте первый блок, чтобы увидеть результат</h3>
  </div>
</template>

<script>
import ResumeTitle from "./ResumeBlocks/ResumeTitle"
import ResumeAvatar from "./ResumeBlocks/ResumeAvatar"
import ResumeSubtitle from "./ResumeBlocks/ResumeSubtitle"
import ResumeText from './ResumeBlocks/ResumeText'

export default {
  name: 'AppView',
  props: ['blocks'],
  components: {
    ResumeTitle, ResumeAvatar, ResumeSubtitle, ResumeText
  },
}
</script>

<style scoped>

</style>