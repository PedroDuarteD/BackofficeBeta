<template >
    <div class="h-full">
 <div class="text-9xl flex	items-center		bg-red-400 justify-center w-full h-screen">
        {{ id }}

 </div>
</div>
</template>
<script >
    export default {
        name: "Project",
        data(){
            return{
                id: this.$route.params.id
            }
        },
    }
</script>