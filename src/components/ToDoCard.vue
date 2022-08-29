<template>
<div id="to_do_card">
    <span :class="getClass(task.status)" class="marginI" @click="edit()" v-if="!task.edit">{{task.message}}</span>
    <input v-model="message" type="text" placeholder="Enter task" v-if="task.edit" class="marginI" v-on:keyup.enter="edit(index)" />
    <ButtonAdd name="Done" class="marginI" v-if="(!task.status)" @click="done()" />
    <ButtonAdd name="Undone" class="marginI" v-if="(task.status)" @click="done()" />
    <ButtonAdd name="Delete" @click="removeTask()" />
</div>
</template>

<script>
import ButtonAdd from './ButtonAdd.vue'

export default {
    props: {
        task: Object,
        index: Number,
        editP: {
            type: Function,
        },
        doneP: {
            type: Function,
        },
        removeTaskP: {
            type: Function,
        },
        editMessage: {
            type: Function,
        },
    },
    comments: {
        ButtonAdd,
    },
    data() {
        return {
            message: this.task.message
        };
    },
    methods: {
        getClass: function (status) {
            return ["card", status ? "done" : "unDone"]
        },
        edit: function () {
            this.editMessage(this.message, this.index)
        },
        done: function () {
            this.doneP(this.index)
        },
        removeTask: function () {
            this.removeTaskP(this.index)
        }
    },
    mounted() {
        this.editMessage(this.message, this.index)
    },
    components: { ButtonAdd }
}
</script>

<style scoped>
div {
    width: 100%;
    display: flex;
    margin-bottom: 16px;
}
.card {
    width: inherit;
    border-radius: .5rem;
    box-sizing: border-box;
    font-family: "Google Sans", Roboto, Arial, sans-serif;
    font-size: .875rem;
    line-height: 1.25rem;
    padding: 16px 24px;
    text-align: left;
    text-decoration-thickness: auto;
    box-shadow: 0 1px 3px 0 #00000080, 0 1px 2px 0 #00000009;
    cursor: pointer;
    font-weight: 900;
    touch-action: manipulation;
}

.card:hover {
    background-color: #ebeef1;
}

.card.done {
    background-color: #1c262c;
}

.card.done:hover {
    background-color: #ebeef1;
}

.card.unDone {
    background-color: #FFFFFF;
}

.card.unDone:hover {
    background-color: #ebeef1;
}

.marginI {
    margin-right: 1%;
}

input {
    width: inherit;
    background-color: #FFFFFF;
    border: 0;
    border-radius: .5rem;
    color: #111827;
    font-size: .875rem;
    padding: 16px 24px;
    outline: 0;
    margin-right: 8px;
    text-decoration: none #D1D5DB solid;
    text-decoration-thickness: auto;
    box-shadow: 0 1px 3px 0 #00000080, 0 1px 2px 0 #00000009;
    user-select: none;
    font-weight: 900;
}

input:focus {
    background-color: #ebeef1;
}
</style>
