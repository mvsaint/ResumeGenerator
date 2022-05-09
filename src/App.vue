<template>
  <div class="container column">
    <app-form 
      @formSubmit="addBlock"
    ></app-form>
    <app-resume
      :blocks="resumeBlocks"
    ></app-resume>
  </div>
  <div class="container">
    <app-comments
      @loadComments="loadComments"
      :comments="comments"
    ></app-comments>
    <app-loader v-if="loading"></app-loader>
  </div>
</template>

<script>
import axios from 'axios'
import AppLoader from "@/components/AppLoader"
import AppComments from "@/components/AppComments"
import AppForm from "@/components/AppForm"
import AppResume from "@/components/AppResume"

export default {
  components: {AppLoader, AppComments, AppForm, AppResume},
  data() {
    return {
      resumeBlocks: [],
      comments: [],
      loading: false
    }
  },
  methods: {
    addBlock(type, value) {
      this.resumeBlocks.push({type, value})
    },
    loadComments() {
      this.loading = true
      setTimeout(async () => {
        try {
          const {data} = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')

          this.comments = Object.keys(data).map(key => {
            return {
              ...data[key]
            }
          })
        } catch (e) {
          console.log(e.message)
        }
      })
    },
    loadPeople() {
      this.loading = true
      setTimeout(async () => {
        try {
          const {data} = await axios.get('https://vue-with-http.firebaseio.com/people.json')
          if (!data) {
            throw new Error('Список людей пуст')
          }

          this.people = Object.keys(data).map(key => {
            return {
              id: key,
              ...data[key]
            }
          })
          this.loading = false
        } catch (e) {
          this.alert = {
            type: 'danger',
            title: 'Ошибка!',
            text: e.message
          }
          this.loading = false
          console.log(e.message)
        }
      }, 1500)
    },
  }
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
