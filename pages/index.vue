<template >
    <div class="bg-neutral-100 py-4 pl-4 pr-4 shadow-xl	">
        <div @click="UpdateCreateProject" class="text-black inline-block p-2 rounded bg-cyan-400	hover:bg-cyan-500	">
          + Project
        </div>
      </div>

      <div  class="pl-4 pr-4 pt-4 ">
        <div v-if="projects.length==0">
          No Project available
        </div>

  <div v-else v-for="project in projects" :key="project.id">
    <CardProject :myproject=project :updateAll= getData></CardProject>
</div>
<AlertDialog v-if="displaycreateProjectForm" :UpdateCreateProject=UpdateCreateProject :getData=getData></AlertDialog>

</div>
</template>
<script >
import  CardProject  from '../components/CardProject.vue';
import  AlertDialog  from '../components/AlertDialog.vue';
    export default {
        name: "Home",
    data(){
      return {
        projects: [],
        displaycreateProjectForm: false
      }
    },
    mounted(){
      this.getData()


    },
    methods: {
      UpdateCreateProject(){
    this.displaycreateProjectForm = !this.displaycreateProjectForm
        
      },
    
      async getData(){

       await fetch("https://backofficebeta.pedroduarte.online/api/allprojects", {method: 'GET',})
       .then((res)=>{
        this.projects = []
          return res.json()
       })
       .then((res)=>{

          this.projects = res


       })
      }

    },
    components: {
      CardProject,
      AlertDialog,
    }
  }
</script>