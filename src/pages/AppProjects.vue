<script>
    import ProjectCard from "../components/ProjectCard.vue"
    import axios from 'axios';
    import { store } from '../store.js';

    export default{
        name: 'AppProjects',
        components: {
            ProjectCard
        },
        data(){
            return {
                store,
                projects: [],
                lastPage: null,
                currentPage: 1,
                isTherePrev: null,
                isThereNext: null,
            };
        },
        methods: {
            getProjectsFromApi(currentPage){
                axios.get(this.store.baseUrl + '/api/projects', 
                { params: {
                    page: currentPage
                }})
                .then((response) => {
                    this.projects = response.data.results.data
                    this.lastPage = response.data.results.last_page
                    this.currentPage = response.data.results.current_page;
                    this.isTherePrev = response.data.results.prev_page_url;
                    this.isThereNext = response.data.results.next_page_url;
                });
            }
        },
        mounted(){
            this.getProjectsFromApi(this.currentPage)
        }
    }
</script>

<template>
    <section>
        <div class="container py-5">
            <div class="row">
                <ProjectCard v-for="project in projects" :projInfo="project"></ProjectCard>
            </div>
            <nav>
              <ul class="pagination mt-5">
                <li class="page-item" :class="{ disabled: !isTherePrev }">
                  <a class="page-link" @click="getProjectsFromApi(currentPage - 1)" aria-label="Previous">
                    <span aria-hidden="true">&laquo;</span>
                  </a>
                </li>
                <li class="page-item" v-for="n in lastPage" :class="{ disabled: currentPage == n }"><a class="page-link" @click="getProjectsFromApi(n)">{{ n }}</a></li>
                <li class="page-item" :class="{ disabled: !isThereNext }">
                  <a class="page-link" @click="getProjectsFromApi(currentPage + 1)" aria-label="Next">
                    <span aria-hidden="true">&raquo;</span>
                  </a>
                </li>
              </ul>
            </nav>
        </div>
    </section>
</template>

<style scoped lang="scss">

    ul.pagination{
        > *:not(.disabled){
            cursor: pointer;
        }
    }

</style>