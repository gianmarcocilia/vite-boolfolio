<script>
import axios from 'axios';

export default {
    data() {
        return {
            url: 'http://127.0.0.1:8000',
            projects: [],
        }
    },
    created() {
        axios.get(`${this.url}/api/projects`).then((resp) => {
            this.projects = resp.data.data;
            console.log(this.projects);
        })
    }
}
</script>

<template>
    <div class="container">
        <h2 class="py-3 text-center">I miei progetti</h2>
        <div class="row row-cols-1 row-cols-md-3 row-cols-lg-4 g-3">
            <div class="col" v-for="project in projects" :key="project.id">
                <div class="card h-100">
                    <div class="card-body">
                        <h4>{{ project.title }}</h4>
                        <img :src="`${url}/storage/${project.project_image}`" alt="">
                        <p>{{ project.description }}</p>
                        <p>Tipologia: <strong>{{ project.type ? project.type.name : 'Non definita'}}</strong></p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>

</style>