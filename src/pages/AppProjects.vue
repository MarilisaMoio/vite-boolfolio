<script>
    import ProjectCard from "../components/ProjectCard.vue"
    import axios from 'axios';

    export default{
        name: 'AppProjects',
        components: {
            ProjectCard
        },
        data(){
            return {
                projects: [],
            }
        },
        methods: {
            getProjectsFromApi(){
                axios.get('http://127.0.0.1:8000/api/projects')
                .then((response) => {
                    this.projects = response.data.results.data
                });
            }
        },
        mounted(){
            this.getProjectsFromApi()
        }
    }
</script>

<template>
    <section>
        <div class="container py-5">
            <div class="row">
                <ProjectCard v-for="project in projects" :projInfo="project"></ProjectCard>
            </div>
        </div>
    </section>
</template>

<style scoped lang="scss">

</style>