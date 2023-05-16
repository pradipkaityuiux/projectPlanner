<template>
  <div>
    <form @submit.prevent="haandleSubmit">
        <label for="title">Title</label>
        <input v-model="title" type="text" id="title" required>
        <label for="details">Details</label>
        <textarea v-model="details" name="details" id="details" cols="30" rows="10" required></textarea>
        <button>Add Project</button>
    </form>
  </div>
</template>

<script>
export default {
    name:"AddProject",
    data(){
        return{
            title: "",
            details:""
        }
    },
    methods:{
        haandleSubmit(){
            let newProject = {
                title: this.title,
                details: this.details,
                complete: false
            }
            fetch('http://localhost:3000/projects',{
                method:"POST",
                headers: {'content-Type': 'application/json'},
                body: JSON.stringify(newProject)
            })
            .then(()=>{
                this.$router.push('/')
            }).catch((err)=> console.log(err.message))
        }
    }
}
</script>

<style>
    form{
        background-color: #fff;
        padding: 20px;
        border-radius: 10px;
    }
    label{
        display: block;
        color: #bbb;
        text-transform: uppercase;
        font-size: 14px;
        font-weight: 900;
        letter-spacing: 1px;
        margin: 20px 0 10px 0;
    }
    input{
        width: 100%;
        padding: 10px;
        border: 0;
        font-size: 16px;
        border-bottom: 1px solid #ddd;
        box-sizing: border-box;
    }
    textarea{
        font-size: 16px;
        border: 1px solid #ddd;
        padding: 10px;
        width: 100%;
        box-sizing: border-box;
        height: 100px;
    }
    form button{
        display: block;
        max-width: 20px auto 0;
        background-color: #00ce89;
        color: #fff;
        padding: 10px;
        border: 0;
        border-radius: 6px;
        font-size: 16px;
        margin-top: 10px;
    }
    input:focus,
    textarea:focus{
        outline: none;
    }
</style>