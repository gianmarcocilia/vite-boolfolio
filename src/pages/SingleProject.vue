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
    <h2 class="text-center py-3">Stai visualizzando il progetto: {{ project.title }}</h2>

</div>
</template>

<style lang="scss" scoped>

</style>