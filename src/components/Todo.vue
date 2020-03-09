<template>
    <table class="table">
        <tr>
            <th>状態</th>
            <th>やること</th>
        </tr>
        <tr v-for="(todo, index) in todos" v-bind:key="todo.id">
            <td><input type="checkbox" true-value="true" false-value="false" v-on:change="changeState(index)" v-model="todo.state"></td>
            <td><span v-bind:class="(todo.state === 'true') ? 'line': ''">{{ todo.title }}</span></td>
        </tr>
    </table>
</template>

<script>
    import { db } from '../main'

    export default {
        data() {
            return {
                todos: [],
            }
        },
        mounted() {
            db.collection('todos').orderBy('createdAt')
                .onSnapshot((snapshot) => {
                    snapshot.docChanges().forEach((change) => {
                        const doc = change.doc
                        if (change.type === 'added') {
                            this.todos.push({id: doc.id, ...doc.data()})
                        }
                    })
                })
        },
        methods: {
            changeState(index) {
                db.collection('todos').doc(this.todos[index].id)
                    .update({state: this.todos[index].state})
                console.log(this.todos[index].state)
            }
        },
    }
</script>

<style scoped>
    .line {
        text-decoration: line-through;
    }
</style>