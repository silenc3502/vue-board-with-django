<template>
    <v-container>
        <div align="center">
            <h2>Vue + Spring 게시판 읽기</h2>
            <board-read-form v-if="board" :board="board"/>
            <p v-else>로딩중 .......... </p>
            <router-link :to="{ name: 'BoardModifyPage', params: { boardId } }">
                게시물 수정
            </router-link>
            <button @click="onDelete">삭제</button>
            <router-link :to="{ name: 'BoardListPage' }">
                돌아가기
            </router-link>
        </div>
    </v-container>
</template>

<script>


import { mapActions, mapState } from 'vuex'
import BoardReadForm from "@/board/read/BoardReadForm.vue";

const boardModule = 'boardModule'

export default {
    components: { BoardReadForm },
    name: "BoardReadPage",
    props: {
        boardId: {
            type: String,
            required: true,
        }
    },
    computed: {
        ...mapState(boardModule, ['board'])
    },
    methods: {
        ...mapActions(boardModule, [
            'requestBoardToSpring',
            'requestDeleteBoardToSpring'
        ]),
        async onDelete () {
            await this.requestDeleteBoardToSpring(this.boardId)
            await this.$router.push({ name: 'BoardListPage' })
        }
    },
    created () {
        console.log('boardId: ' + this.boardId)
        this.requestBoardToSpring(this.boardId)
    }
}

</script>

<style>

</style>