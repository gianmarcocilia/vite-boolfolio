<script>
import axios from 'axios';
import { store } from '../store';
export default {
    data() {
        return {
            store,
            project: null,
        }
    },
    created() {
        axios.get(`${store.baseUrl}/api/projects/${this.$route.params.slug}`).then((resp) => {
        this.project = resp.data;
      })
    }
}
</script>

<template>
<div class="container" v-if="project">
    <h2 class="py-3">Stai visualizzando il progetto: {{ project.title }}</h2>
    <p class="py-1">{{ project.description }}</p>
    <img v-if="project.project_image" :src="`${store.baseUrl}/storage/${project.project_image}`" alt="">
    
    <ul>
        <li>Tipologia: {{ project.type ? project.type.name : 'Non definita' }}</li>
        <li v-if="project.technologies.length > 0">
            Tecnologie:
            <ul>
                <li v-for="technology in project.technologies">{{ technology.name }}</li>
            </ul>
        </li>
        <li v-else>Tecnologie non definite.</li>
    </ul>

    <p class="fs-6 pt-5">Made by {{ project.user.name }}, email: <strong>{{ project.user.email }}</strong></p>
</div>
</template>

<style lang="scss" scoped>

</style>