<template>
    <v-container>
        <div align="center">
            <h2>게시물 수정</h2>
            <board-modify-form v-if="board" :board="board" @submit="onSubmit"/>
            <p v-else>로딩중 ........</p>
        </div>
    </v-container>
</template>

<script>

import { mapActions, mapState } from 'vuex'
import BoardModifyForm from "@/board/modify/BoardModifyForm.vue";

const boardModule = 'boardModule'

export default {
    components: { BoardModifyForm },
    name: "BoardModifyPage",
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
            'requestBoardModifyToSpring',
        ]),
        async onSubmit (payload) {
            const { title, content, writer } = payload
            const boardId = this.boardId

            await this.requestBoardModifyToSpring({ boardId, title, content, writer })
            await this.$router.push({
                name: 'JpaBoardReadPage',
                params: { boardId: this.boardId }
            })
        }
    },
    created () {
        this.requestBoardToSpring(this.boardId)
    }
}

</script>

<style>

</style>