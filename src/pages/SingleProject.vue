<script>
    import axios from 'axios';
    import { store } from '../store.js';

    export default{
        name: 'SingleProject',
        data() {
            return{
                store,
                project: null
            }
        },
        methods: {
            getSingleProjectFromApi(){
                axios.get(this.store.baseUrl + '/api/projects/' + this.$route.params.slug )
                .then((response) => {
                    this.project = response.data.project
                    console.log(this.project)
                });
            }
        },
        mounted(){
            this.getSingleProjectFromApi()
        }
    }
</script>

<template>
    <section>
        <div class="container">
            <div v-if="project">
                <h5>{{ project.name }}</h5>
                <div>Tipo: {{ project.type ? project.type.name : "---" }}</div>
                <div>For: {{ project.client_name ? project.client_name : "---" }}</div>
                <div class="owl" v-if="project.technologies">
                    <span class="badge rounded-pill bg-primary" v-for="tech in project.technologies">{{ tech.name }}</span>
                </div>
                <p class="card-text" v-if="project.summary">{{ project.summary }}</p>
            </div>
            
        </div>
    </section>
</template>

<style scoped lang="scss">
    .owl{
        > * + *{
            margin-left: 6px
        }
    }
</style>