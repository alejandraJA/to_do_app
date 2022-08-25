<template>
<nav class="nav">
    <ul>
        <li id="title">
            <h1>To do</h1>
        </li>
        <li v-for="(item) in filters" :key="item" v-text="item.message" :class="filterClass(item.selected)" @click="filter(item)" />
    </ul>
</nav>
<section id="add">
    <input v-model="task" type="text" placeholder="Enter task">
    <ButtonAdd name="Add" @click="addTask()" />
</section>

<section id="toDoCards" v-for="(task) in tasks" :key="task">
    <ToDoCard :task="task" v-if="task.view" />
</section>
</template>

<script>
import ButtonAdd from './components/ButtonAdd.vue';
import ToDoCard from './components/ToDoCard.vue';
export default {
    name: 'App',
    components: {
        ButtonAdd,
        ToDoCard
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
                    message: "Undone",
                    selected: false
                },
            ],
            tasks: [{
                message: "Aprender css",
                status: false,
                edit: false,
                view: true
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
            if (this.task != null) {
                this.tasks.push({
                    message: this.task,
                    status: false,
                    edit: false,
                    view: true
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
        }
    }
}
</script>

<style>
#app {
    font-family: "Google Sans", Roboto, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    text-align: center;
    margin-top: 5%;
    margin-left: 5%;
    margin-right: 5%;
    margin-bottom: 5%;
}

#title {
    width: wrap;
    color: #111827;
    font-size: 16px;
    letter-spacing: -0.047em;
    cursor: default;
}

#add {
    margin-bottom: 32px;
}

ul {
    list-style-type: none;
}

li {
    display: inline-block;
    padding: 16px;
    cursor: pointer;
}

input {
    background-color: #FFFFFF;
    border: 0;
    width: 35%;
    border-radius: .5rem;
    box-sizing: border-box;
    color: #111827;
    font-size: .875rem;
    padding: 16px 24px;
    margin-right: 8px;
    text-decoration: none #D1D5DB solid;
    text-decoration-thickness: auto;
    box-shadow: 0 1px 3px 0 #00000080, 0 1px 2px 0 #00000009;
    user-select: none;
    -webkit-user-select: none;
    font-weight: 900;
    touch-action: manipulation;
}

input:hover {
    background-color: #ebeef1;
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
