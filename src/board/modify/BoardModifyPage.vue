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
    data() {
        return {
            isSubmitting: false
        }
    },
    methods: {
        ...mapActions(boardModule, [
            'requestBoardToSpring',
            'requestModifyBoardToSpring',
        ]),
        async onSubmit (payload) {
            if (!this.isSubmitting) {
                this.isSubmitting = true;
                const { title, content, writer } = payload
                const boardId = this.boardId

                try {
                    await this.requestModifyBoardToSpring({ boardId, title, content, writer })
                    await this.$router.push({
                        name: 'BoardReadPage',
                        params: { boardId: this.boardId }
                    })
                } catch (error) {
                    console.error('Error occurred while submitting:', error);
                } finally {
                    this.isSubmitting = false; // 제출 완료 후 상태 변경
                }
            }
        }
    },
    created () {
        this.requestBoardToSpring(this.boardId)
    }
}

</script>

<style>

</style>