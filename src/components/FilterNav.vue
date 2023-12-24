<template>
<nav class="filter-nav">
    <button @click="updatefilter('all')" :class="{active: current === 'all'}">Viwe All</button>
    <button @click="updatefilter('completed')" :class="{active: current === 'completed'}">Completed</button>
    <button @click="updatefilter('ongoing')" :class="{active: current === 'ongoing'}">Ongoing</button>
</nav>
</template>

<script>
export default {
    props:['current'],
    methods:
    {
        updatefilter(by)
        {
            this.$emit('filterchange' , by)
        }
    }
}
</script>

<style>
.filter-nav button
{
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
}
.filter-nav button.active
{
color:#555
}
</style>