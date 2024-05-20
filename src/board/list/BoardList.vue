<template>
  <div>
    <h3>게시물 목록</h3>
    <table>
      <thead>
      <tr>
        <th align="center" width="100">No</th>
        <th align="center" width="640">제목</th>
        <th align="center" width="150">작성자</th>
        <th align="center" width="300">등록일자</th>
      </tr>
      </thead>
      <tbody>
      <tr v-if="!boards || (Array.isArray(boards) && boards.length === 0)">
        <td colspan="4">
          현재 등록된 게시물이 없습니다!
        </td>
      </tr>
      <tr v-else v-for="board in boards" :key="board.boardId">
        <td align="center">
          {{ board.boardId }}
        </td>
        <td align="left">
          <router-link :to="{ name: 'JpaBoardReadPage', params: { boardId: board.boardId.toString() } }">
            {{ board.title }}
          </router-link>
        </td>
        <td align="right">
          {{ board.writer }}
        </td>
        <td align="center">
          {{ board.regDate }}
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  boards: {
    type: Array,
    required: false,
    default: () => []
  }
});
</script>

<style scoped>
/* 스타일을 여기에 추가할 수 있습니다. */
</style>


