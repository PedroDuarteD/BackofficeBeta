

<template >
    <div >
       

<div class="p-4 rounded mb-2"  :class="project.show=='1' && project.prod==1? 'bg-emerald-300' : 'bg-slate-300	'">

  <div class="flex">
    <div class="w-1/2"> <NuxtLink :to="'project/3'">
<div class="text-2xl mb-1">{{ project.name }}</div>
  <div>{{ project.desc }}</div></NuxtLink>
    </div>

<div  class="flex items-end justify-end	w-1/2 pb-4">
<button @click="()=>updateVisibility(project.id, 'show', project.show==1? 0 : 1)" class="text-white p-2 rounded bg-green-500	 mr-4	" :class="project.show!=1? 'bg-stone-600	hover:bg-stone-700	' : 'hover:bg-green-600'">Show  </button>
<button @click="()=>updateVisibility(project.id, 'prod', project.prod==1? 0 : 1)" class="text-white p-2 rounded		" :class="project.prod!=1? '	bg-gray-400 hover:bg-gray-700		' : ' bg-teal-400	 hover:bg-teal-600'">Production </button>
<button @click="()=>DeleteProject(project.id)" class="text-white p-2 rounded bg-red-600	ml-4	hover:bg-red-800" >Delete</button>
    </div>

    
  </div>

</div>


</div>
</template>
<script >
    export default {
        name: "CardProject",
        data(){
            return{
                project: this.myproject
            }
        },
        methods: {
            
            async DeleteProject(id){
        await fetch("https://backofficebeta.pedroduarte.online/api/deleteproject?id="+id,{method: "delete"})
        .then((response)=>{
            this.updateAll()
        })
      },
    async  updateVisibility(id, type, value){
        await fetch("https://backofficebeta.pedroduarte.online/api/updateVisibility?id="+id+"&type="+type+"&value="+value, {method: 'PUT'})
       .then((res)=>{
        this.updateAll()
       })
      },
        },
        props: [
            "myproject",
            "updateAll"
        ]
    }
</script>