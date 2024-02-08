<template >
    <div class="m-0 p-0" >
        <div  class="bg-stone-950	 bg-opacity-40	 flex	flex-col justify-center		fixed w-full h-full top-0 left-0">
        <center>
            <div class="bg-white	rounded w-1/5 pl-2 pr-2 h-auto pb-4">
              <div  class="flex pt-4 mb-2">  create Project</div>

              <div style="display: flex;flex-direction: column; align-items: start;margin-bottom: 1vh;">
                <label>Name</label>
                <input class="mt-2 text-base	rounded w-11/12	p-2 border-2" type="text" v-model="name" >
                <div class="text-red-500	text-base mt-1" v-if="name_v">Need to fill with Name</div>
              </div>


              <div style="display: flex;flex-direction: column; align-items: start;margin-bottom: 1vh;">
                <label>Description</label>
                <input  class="mt-2 text-base	rounded w-11/12	p-2  border-2" type="text" v-model="desc" >
                <div class="text-red-500	text-base mt-1" v-if="desc_v">Need to fill with Description</div>

              </div>

              <div style="display: flex; align-items: start;;margin-bottom: 1vh;">
                <label style="margin-right: 0.5vw;">Show</label>
                <input type="checkbox" v-model="show" >

              </div>


              <div style="display: flex; align-items: start;;margin-bottom: 1vh;">
                <label style="margin-right: 0.5vw;">Production</label>
                <input type="checkbox" v-model="prod" >

              </div>

              <div style="display: flex; justify-content: space-evenly;">
                <button class="text-white	p-2 rounded inline-block bg-gray-800	hover:bg-gray-600 	" @click="btnCancel">Cancelar</button>
                <button class="text-white inline-block p-2 bg-green-500	rounded" @click="btnCreate">Criar</button>
              </div>
        
        </div>
        </center>
      
      </div>
</div>
</template>

<script>
export default {
  data(){
    return{
        name: "",
        desc: "",
        show: true,
        prod: false,
        name_v: false,
        desc_v: false
    }
  },
  methods: {
    btnCancel(){
      this.UpdateCreateProject()
    },
   async btnCreate(){
    if(this.name==""){
    this.name_v = true
  }else{
    this.name_v = false
  }

  if(this.desc==""){
    this.desc_v = true
  }else{
    this.desc_v = false
  }
        if(this.name_v==false && this.desc_v==false ){

       
 await $fetch("https://backofficebeta.pedroduarte.online/api/addproject",{
  
  body: {
    name: this.name,
    desc: this.desc,
    prod: this.prod,
    show: this.show
  },
  method: "POST"
}).then((response)=>{
  if(response.includes("Success")){
   this.UpdateCreateProject()
    this.getData()
    this.name = ""
    this.desc=""

  }
})

}
    }
  },
  props: [
  "UpdateCreateProject",
  "getData",
  ]
}
</script>
