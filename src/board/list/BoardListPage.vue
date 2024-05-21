<template>
    <v-container>
        <h2>Vue + Spring + JPA Boards</h2>
        <router-link :to="{ name: 'BoardRegisterPage' }">
            게시물 작성
        </router-link>
        <board-list-form :boards="boards"/>
    </v-container>
</template>

<script>

import { mapActions, mapState } from 'vuex'
import BoardListForm from "@/board/list/BoardListForm.vue";

const boardModule = 'boardModule'

export default {
    components: {BoardListForm},
    name: "JpaBoardListPage",
    computed: {
        ...mapState(boardModule, ['boards']),
    },
    mounted () {
        this.requestBoardListToSpring()
    },
    methods: {
        ...mapActions(boardModule, [
            'requestBoardListToSpring'
        ])
    }
}

</script>

<style>

</style>