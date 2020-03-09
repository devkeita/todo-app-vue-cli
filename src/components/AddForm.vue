<template>
    <input type="text" v-model="newTodo" v-on:keydown.enter="addTodo" class="form-control">
</template>

<script>
    import { db } from '../main.js'

    export default {
        data() {
            return {
                newTodo: null,
            }
        },
        methods: {
            addTodo(event) {
                if (this.newTodo === null) {return}
                if (this.keyDownedForJPConversion(event)) {return}
                db.collection('todos').add({title: this.newTodo, state: false, createdAt: new Date().getTime()})
                this.newTodo = null
            },
            keyDownedForJPConversion(event) {
                const codeForConversion = 229
                return event.keyCode === codeForConversion
            }
        }
    }
</script>

<style scoped>

</style>