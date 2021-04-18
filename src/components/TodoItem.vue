<template>
    <li>
        <span v-bind:class='{done: todo.completed}'>
            <input type="checkbox" v-on:change="todo.completed=!todo.completed">
            <strong> {{index+1}} </strong>
            {{todo.title | uppercase}}
        </span>
        <button class="btn" v-on:click="$emit('remove-todo',todo.id)">&times;</button>
         </li>
</template>
<script>
export default {
    props: {
        todo: {
            type:Object,
            required:true
        },
        index:Number
    },
    filters: {
        uppercase(value) {
            return value.toUpperCase()
        }
    }
}
</script>
<style scoped>
li {
    border: 1px solid black;
    display: flex;
    justify-content: space-between;
    padding: 10px 20px;
    margin-bottom: 5px;

}
input {
    margin-right: 10px;
}

.btn {
    background: red;
    color: white;
    border-radius: 50%;
    font-weight: bold;
}
.done {
    text-decoration: line-through;
}

</style>