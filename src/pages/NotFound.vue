<script>
export default {
    data() {
        return {

        }
    }
}
</script>

<template>
    <div class="container">
        <h2 class="text-center py-3">Error 404 - Page not found.</h2>
        <div class="d-flex justify-content-center">
            <router-link :to="{name: 'home'}" class="btn btn-primary">Torna alla Home</router-link>
        </div>
    </div>
</template>

<style lang="scss" scoped>

</style>