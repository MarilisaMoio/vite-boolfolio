<script>
    export default{
        name: 'ProjectCard',
        props: ['projInfo'],
        methods: {
            //funzioncina per far troncare la frase sempre alla fine di una parola
            truncSummary(summary){
                let startingPoint = 100;
                let truncPoint = 0;

                let findWhitespace = false;
                while(!findWhitespace){
                    if(summary[startingPoint] == " "){
                        findWhitespace = true;
                        truncPoint = startingPoint - 1
                    } else {
                        startingPoint++
                    }
                }

                let trunSum = summary.substr(0, truncPoint);

                return trunSum;
            }
        }
    }
</script>

<template>
    <div class="col-4">
        <div class="card" style="width: 18rem;">
            <!-- non metto le immagini giusto perché ne ho solo 1 sul db -->
            <div class="card-body">
                <h5 class="card-title">{{ projInfo.name }}</h5>
                <div>Tipo: {{ projInfo.type ? projInfo.type.name : "---" }}</div>
                <div class="owl" v-if="projInfo.technologies">
                    <span class="badge rounded-pill bg-primary" v-for="tech in projInfo.technologies">{{ tech.name }}</span>
                </div>
                <p class="card-text" v-if="projInfo.summary">{{ projInfo.summary.length > 100 ? truncSummary(projInfo.summary) + '...' : projInfo.summary }}</p>
            </div>
            <div class="card-footer">
                <router-link class="btn btn-primary" :to="{ name: 'single-project', params: { slug: projInfo.slug } }">Vedi i dettagli</router-link>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
    .owl{
        > * + *{
            margin-left: 6px
        }
    }

    .card{
        height: 300px;
    }

</style>