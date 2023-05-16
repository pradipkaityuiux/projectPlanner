<template>
  <div>
    <form @submit.prevent="handleEdit">
        <label for="title">Title</label>
        <input v-model="title" type="text" id="title" required>
        <label for="details">Details</label>
        <textarea v-model="details" name="details" id="details" cols="30" rows="10" required></textarea>
        <button>Edit Project</button>
    </form>
  </div>
</template>

<script>
export default {
    name:"EditProject",
    props:["id"],
    data(){
        return{
            title: "",
            details:"",
            url: "http://localhost:3000/projects/"+this.id
        }
    },
    mounted(){
        fetch(this.url)
            .then(response => response.json())
            .then((data)=>{
                this.title = data.title,
                this.details = data.title
            })
    },
    methods:{
        handleEdit(){
            fetch(this.url,{
                method: "PATCH",
                headers: {'content-Type': 'application/json'},
                body:JSON.stringify({title:this.title, details: this.details })
            })
            .then(()=>{
                this.$router.push('/')
            }).catch((err)=> console.log(err.message))
        }
    }

}
</script>

<style>

</style>
