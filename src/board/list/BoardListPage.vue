<template>
  <v-container>
    <h2>Vue + Django Boards</h2>
    <router-link :to="{ name: 'BoardRegisterPage' }">
      게시물 작성
    </router-link>
    <board-list-form :boards="boards"/>
  </v-container>
</template>

<script setup lang="ts">
import { computed, onMounted } from 'vue'
import { useStore } from 'vuex'
import { useRouter } from 'vue-router'
import BoardListForm from "@/board/list/BoardListForm.vue";

const store = useStore()
const router = useRouter()

const boards = computed(() => store.state.boardModule.boards)

const requestBoardListToSpring = () => {
  store.dispatch('boardModule/requestBoardListToSpring')
}

onMounted(() => {
  requestBoardListToSpring()
})
</script>

<style scoped>
</style>
