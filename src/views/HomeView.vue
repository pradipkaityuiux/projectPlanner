<template>
  <div class="home">
    <FilteredView @filter="currentFilter=$event" :current="currentFilter"/>
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject :project="project" @delete="deleteProject" @complete="completeProject"/>
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject.vue";
import FilteredView from "../views/FilteredView.vue";
export default {
  name: 'HomeView',
  components: {SingleProject, FilteredView},
  data(){
    return{
      projects:[],
      currentFilter: 'all',
    }
  },
  mounted(){
    fetch("http://localhost:3000/projects")
      .then(response => response.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err.message))
  },
  methods:{
    deleteProject(id){
      this.projects = this.projects.filter((task)=>{
        return task.id != id
      })
    },
    completeProject(id){
      let p = this.projects.find( project=>{
        return project.id === id
      })
      p.complete = !p.complete
    }
  },
  computed:{
    filteredProjects(){
      if(this.currentFilter=='complete'){
        return this.projects.filter((project)=> project.complete)
      }
      if(this.currentFilter=='onGoing'){
        return this.projects.filter((project)=> !project.complete)
      }
      return this.projects
    }
  }
}
</script>
