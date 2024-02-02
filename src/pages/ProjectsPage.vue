<script>
import axios from 'axios';
import { store } from '../store';
import ProjectCard from '../components/ProjectCard.vue';
import AppLoader from '../components/AppLoader.vue';

export default {
    data() {
        return {
            store,
            projects: [],
            loading: false
        };
    },
    created() {
        this.loading = true;
        axios.get(`${this.store.baseUrl}/api/projects`).then((resp) => {
            console.log(resp);
            this.projects = resp.data.data;
            this.loading = false;
        });
    },
    components: { ProjectCard, AppLoader }
}
</script>

<template>
    <div class="container">
        <h2 class="py-3 text-center">I miei progetti</h2>
        <div v-if="loading">
            <AppLoader />
        </div>
        <div v-else class="row row-cols-1 row-cols-md-3 row-cols-lg-4 g-3 pb-3">
            <div class="col" v-for="project in projects" :key="project.id">
                <ProjectCard :project="project"/>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>

</style>