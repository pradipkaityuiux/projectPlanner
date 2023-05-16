<template>
    <div class="project" :class="{'taskFininsh': project.complete}">
        <div class="actions">
            <h3 @click="this.hideDetails = !this.hideDetails">{{ project.title }}</h3>

            <div class="icons">
                <router-link :to="{name: 'EditProject', params:{ id: project.id }}">
                    <Icon icon="mdi:square-edit-outline" />
                </router-link>
                <Icon icon="material-symbols:delete-outline" @click="deleteProject"/>
                <Icon icon="material-symbols:done" @click="toggleComplete" :class="{'projectFininsh': project.complete}"/>
            </div>
        </div>
        <div class="details" v-if="this.hideDetails">
            <p>{{ project.details }}</p>
        </div>
    </div>
    <!--    https://docs.iconify.design/icon-components/vue/          (Iconify Documentation) -->
</template>

<script>
import { Icon } from '@iconify/vue';
export default {
    name: "SingleProject",
    props:["project"],
    components:{Icon},
    data(){
        return{
            hideDetails:false,
            url: "http://localhost:3000/projects/" + this.project.id
        }
    },
    methods:{
        deleteProject(){
            fetch(this.url, { method: "DELETE" })
            .then(()=>{this.$emit('delete', this.project.id)})
            .catch(err=> console.log(err.message))
        },
        toggleComplete(){
            fetch(this.url, { 
                method: "PATCH",
                headers: {'content-Type': 'application/json'},
                body: JSON.stringify({complete: !this.project.complete})
            })
            .then(()=>{this.$emit('complete', this.project.id)}) 
            .catch((err)=>console.log(err.message))
        }
    }
}
</script>

<style scoped>
    .project{
        margin: 20px auto;
        background-color: #fff;
        padding: 10px 20px;
        border-radius: 4px;
        box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
        border-left: 4px solid #e90074;
    }
    .project.taskFininsh{
        border-left: 4px solid #00ce89;
    }
    .actions{
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .icons svg{
        color: #b1b1b1;
        cursor: pointer;
        height: 24px;
        width: 24px;
        transition: 0.3s ease-in-out;
        padding: 8px;
        border-radius: 50%;
    }
    .icons svg:hover{
        color: #444444;
        background-color: #f1f1f1;
    }
    h3{
        cursor: pointer;
    }
    .icons svg.projectFininsh{
        color: #00dd63;
        background-color: #d4ffe8;
    }
</style>