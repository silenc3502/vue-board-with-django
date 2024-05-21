<template>
    <v-container>
        <h2>게시물 작성</h2>
        <board-register-form @submit="onSubmit"/>
    </v-container>
</template>

<script>

import { mapActions } from 'vuex'
import BoardRegisterForm from "@/board/register/BoardRegisterForm.vue";

const boardModule = 'boardModule'

export default {
    components: { BoardRegisterForm },
    name: "BoardRegisterPage",
    methods: {
        ...mapActions (boardModule, [
            'requestCreateBoardToSpring'
        ]),
        async onSubmit (payload) {
            if (payload.title) {
                console.log('onSubmit payload:', payload);
                const board = await this.requestCreateBoardToSpring(payload)
                // console.log('board: ' + JSON.stringify(board.data))
                console.log('board:', board);
                await this.$router.push({
                    name: 'BoardReadPage',
                    params: {boardId: board.boardId.toString()}
                })
            }
        }
    }
}

</script>

<style>

</style>