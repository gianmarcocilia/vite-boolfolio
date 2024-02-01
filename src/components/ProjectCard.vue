<script>
export default {
    props: {
        project: Object,
        url: String
    },
    data() {
        return {

        }
    },
}
</script>

<template>
    <div class="card h-100">
        <div class="card-body">
            <h4>{{ project.title }}</h4>
            <img :src="`${url}/storage/${project.project_image}`" alt="">
            <p>{{ project.description }}</p>
            <p>Tipologia: <strong>{{ project.type ? project.type.name : 'Non definita' }}</strong></p>
        </div>
    </div>
</template>

<style lang="scss" scoped></style>