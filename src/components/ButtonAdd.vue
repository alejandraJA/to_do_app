<template>
<button class="button" v-text="name" />
</template>

<script>
export default {
    props: {
        name: String
    }
}
</script>

<style scoped>
.button {
    background-color: #FFFFFF;
    border: 0;
    border-radius: .5rem;
    box-sizing: border-box;
    color: #111827;
    font-family: "Google Sans", Roboto, Arial, sans-serif;
    font-size: .875rem;
    line-height: 1.25rem;
    padding: 16px 24px;
    text-align: center;
    text-decoration: none #D1D5DB solid;
    text-decoration-thickness: auto;
    box-shadow: 0 1px 3px 0 #00000080, 0 1px 2px 0 #00000009;
    cursor: pointer;
    user-select: none;
    -webkit-user-select: none;
    font-weight: 900;
    touch-action: manipulation;
}

.button:hover {
    background-color: #ebeef1;
}

.button:focus {
    outline: 2px solid transparent;
    outline-offset: 2px;
}

.button:focus-visible {
    box-shadow: none;
}
</style>
