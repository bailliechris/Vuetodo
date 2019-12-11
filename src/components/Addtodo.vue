<template>
    <div>
        <form @submit="addTodo">
            <input type="text" name="title" v-model="title" placeholder="Add a job...">
            <input type="submit" value="Add" class="btn">
        </form>
    </div>
</template>

<script>
import uuid from "uuid";

export default {
    name:"Addtodo",
    data() {
        return {
            title:""
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault();
            const newTodo = {
                id: uuid.v4(),
                title: this.title,
                completed: false
            }
            //Send to parent
            this.$emit('add-todo', newTodo);

            this.title = "";
        }
    }
}
</script>

<style scoped>
form {
    display: flex;
}

input[type="text"]{
    flex:10;
    padding:5px;
}

input[type="submit"]{
    flex:2;
}
</style>