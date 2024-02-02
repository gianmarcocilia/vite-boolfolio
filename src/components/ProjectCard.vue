<script>
import { store } from '../store';

export default {
    props: {
        project: Object,
    },
    data() {
        return {
            store
        }
    },
    computed: {
        truncateDescription() {
            if (this.project.description && this.project.description.length > 250) {
        return this.project.description.substring(0, 150) + "...";
      }
      return this.project.description;
        }
    }
}
</script>

<template>
    <div class="card h-100">
        <div class="card-body">
            <h4>{{ project.title }}</h4>
            <img :src="`${store.baseUrl}/storage/${project.project_image}`" alt="">
            <p>{{ truncateDescription }}</p>
            <p>Tipologia: <strong>{{ project.type ? project.type.name : 'Non definita' }}</strong></p>
        </div>
    </div>
</template>

<style lang="scss" scoped></style>