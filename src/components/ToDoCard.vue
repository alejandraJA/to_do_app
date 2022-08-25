<template>
<div id="to_do_card" :class="getClass(task.status)" >
    <span>{{task.message}}</span>
</div>
</template>

<script>
export default {
    props: {
        task: Object
    }, 
    methods: {
        getClass: function (status) {
            return ['card', status ? 'done' : 'unDone']
        },
    },
}
</script>

<style>
.card {
    width: 100%;
    border-radius: .5rem;
    box-sizing: border-box;
    font-family: "Google Sans", Roboto, Arial, sans-serif;
    font-size: .875rem;
    line-height: 1.25rem;
    padding: 16px 24px;
    text-align: left;
    text-decoration-thickness: auto;
    box-shadow: 0 1px 3px 0 #00000080, 0 1px 2px 0 #00000009;
    cursor: text;
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

</style>
