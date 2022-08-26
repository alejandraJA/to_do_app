<template>
<nav class="nav">
    <ul>
        <li id="title">
            <h1>To do</h1>
        </li>
        <li v-for="(item) in filters" :key="item" v-text="item.message" :class="filterClass(item.selected)" @click="filter(item)" />
    </ul>
</nav>


<section class="container">
    <p v-text="'Done ' + doneCount + ' Undone ' + undone" />
    <section id="add">
        <input v-model="task" type="text" placeholder="Enter task" v-on:keyup.enter="addTask()">
        <ButtonAdd name="Add" @click="addTask()" />
    </section>

    <ToDoCard v-for="(task, index) in taskFilter" :key="task" :task="task" :index="index" :editP="edit" :doneP="done" :removeTaskP="removeTask" :editMessage="editMessage" />
    
</section>
</template>

<script>
import ButtonAdd from './components/ButtonAdd.vue';
import ToDoCard from './components/ToDoCard.vue';

export default {
    name: 'App',
    components: {
        ButtonAdd,
        ToDoCard,
    },
    data() {
        return {
            filterPropiety: "All",
            task: "",
            filters: [{
                    message: "All",
                    selected: true
                },
                {
                    message: "Done",
                    selected: false
                },
                {
                    message: "undone",
                    selected: false
                },
            ],
            tasks: [{
                message: "Aprender css 1",
                status: false,
                edit: false,
            }, ]
        }
    },
    methods: {
        filterClass: function (status) {
            return ['filter', status ? 'checked' : 'unchecked']
        },
        filter: function (item) {
            this.filters[0].selected = false
            this.filters[1].selected = false
            this.filters[2].selected = false
            item.selected = true
            this.filterPropiety = item.message
            return
        },
        addTask: function () {
            if (this.task.length >= 1) {
                this.tasks.push({
                    message: this.task,
                    status: false,
                    edit: false,
                })
                this.filterPropiety = "all"
                this.filters[0].selected = true
                this.filters[1].selected = false
                this.filters[2].selected = false
                this.task = ""
            } else {
                // TODO
            }
            return
        },
        edit: function (index) {
            this.tasks[index].edit = !this.tasks[index].edit
            return
        },
        done: function (index) {
            this.tasks[index].edit = false
            this.tasks[index].status = !this.tasks[index].status
            return
        },
        removeTask: function (index) {
            this.tasks.splice(index, 1)
            return
        },
        editMessage(message, index) {
            this.tasks[index].edit = !this.tasks[index].edit
            this.tasks[index].message = message
            return
        }
    },
    computed: {
        taskFilter: function () {
            if (this.filterPropiety == 'undone') {
                return this.tasks.filter(function (task) {
                    return !task.status
                })
            }
            if (this.filterPropiety == 'Done') {
                return this.tasks.filter(function (task) {
                    return task.status
                })
            } else {
                return this.tasks
            }
        },
        doneCount: function () {
            return this.tasks.filter(function (task) {
                return task.status
            }).length
        },
        undone: function () {
            return this.tasks.filter(function (task) {
                return !task.status
            }).length
        }
    },
}
</script>

<style scoped>
#app {
    font-family: "Google Sans", Roboto, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    text-align: center;
}

#title {
    width: wrap;
    color: #111827;
    font-size: 16px;
    letter-spacing: -0.047em;
    cursor: default;
}

.container {
    margin-right: 20%;
    margin-left: 20%;
}

#add {
    width: 100%;
    display: flex;
    margin-bottom: 16px;
}

nav {
    margin-right: 20%;
    margin-left: 20%;
}

ul {
    padding-left: 0px;
}

li {
    display: inline-block;
    padding: 16px;
    cursor: pointer;
}

input {
    background-color: #FFFFFF;
    border: 0;
    width: 100%;
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

.filter {
    border: 0;
    border-radius: .5rem;
    box-sizing: border-box;
    color: #111827;
    font-size: .875rem;
    padding: 16px 24px;
    margin-right: 8px;
    text-decoration: none #D1D5DB solid;
    text-decoration-thickness: auto;
    user-select: none;
    -webkit-user-select: none;
    font-weight: 900;
    touch-action: manipulation;
}

.filter.checked {
    background-color: #ebeef1;
    box-shadow: 0 1px 3px 0 #00000080, 0 1px 2px 0 #00000009;
}

.filter.unchecked {
    border: 0;
    border-radius: .5rem;
    box-sizing: border-box;
    color: #111827;
    font-size: .875rem;
    padding: 16px 24px;
    margin-right: 8px;
    text-decoration: none #D1D5DB solid;
    text-decoration-thickness: auto;
    user-select: none;
    -webkit-user-select: none;
    font-weight: 900;
    touch-action: manipulation;
}
</style>
