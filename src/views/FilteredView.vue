<template>
  <div>
    <div class="filter">
        <button :class="{active: current=='all'}" @click="filter('all')">All</button>
        <button :class="{active: current=='onGoing'}" @click="filter('onGoing')">Onging</button>
        <button :class="{active: current=='complete'}" @click="filter('complete')">Completed</button>
    </div>
  </div>
</template>

<script>
export default {
    name:"FilteredView",
    props:["current"],
    methods:{
        filter(filterBy){
            this.$emit('filter', filterBy)
        }
    }
}
</script>

<style scoped>
    button{
        font-weight: 800;
        color: #8a8a8a;
        border: none;
        background-color: transparent;
        font-size: 16px;
        margin: 10px;
        cursor: pointer;
    }
    .active{
        color: #4d4d4d;
    }
</style>