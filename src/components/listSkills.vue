<template>
    <div class="w-full sm:w-11/12 bg-gray-100 mx-auto pt-4 sm:p-4 rounded-lg">
        <h2 class="text-3xl">{{ selectedOption.title }}</h2>
        <h2 class="text-xl" v-if="selectedOption.title == 'Projects'">
            *Note -> I know that all of these projects are not perfect, code could be clearer and the view could look better. I'm still learning !:)
        </h2>
        <div class="flex flex-wrap space-y-1 ">
            <div v-for="skill in selectedOption">
                <div v-if="skill.name && !skill.url" class="p-4 m-4 flex items-center bg-gray-200  flex-col border-2 border-gray-300 rounded-md w-11/12 mx-auto sm:w-72 h-full sm:h-96 relative sm:mx-1">
                    <div v-if="!skill.url" class="h-full">
                        <div class="h-1/3 flex items-center flex-col w-full">
                            <div v-if="skill.rating" class="flex space-x-1 ">
                                <img v-for="num in skill.rating" class="h-3 mt-1" src="/src/assets/img/icons/star.png" alt="">
                            </div>
                            <h2 class="text-3xl break-all ">{{skill.name}}</h2>
                            <img class="h-24" :src="`/src/assets/img/icons/${skill.img}`" alt="">
                        </div>
                        <div class="h-2/3 mt-8  flex items-center justify-center">
                            <p class="pt-2">{{skill.desc}}</p>
                        </div>
                    </div>

                </div>
                <div v-if="skill.url" class="p-4 sm:m-4 flex items-center bg-gray-200  flex-col border-2 border-gray-300 rounded-md w-full sm:w-96  h-full sm:h-96 relative">
                    <div class="h-full">
                        <ProjectCard :skillData="skill"/>
                    </div>
                    <div class="bg-green-500 border border-green-700 px-2  text-white absolute right-0 bottom-0 rounded-md" v-if="skill.commercial">
                        Commercial project
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import skills from '/src/skills.json'
import ProjectCard from '/src/components/ProjectCard.vue'
    export default {
        components:{
            ProjectCard,
        },
        data() {
            return {
                skills:skills,
            }
        },
        computed:{
            selectedOption(){
                if(!this.$route.params.details){
                return  this.skills["frontEnd"];
                }
                return  this.skills[this.$route.params.details];
            }
        }
    }
</script>

<style  scoped>

</style>