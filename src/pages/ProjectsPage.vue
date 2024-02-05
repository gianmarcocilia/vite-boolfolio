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
            loading: false,
            curPage: 1,
            totPage: 1
        };
    },
    created() {
        this.getProjectsPage(1);
    },
    methods: {
        getProjectsPage(pageNum) {
            this.loading = true;
            this.curPage = pageNum;
            axios.get(`${this.store.baseUrl}/api/projects`, {
                params: {
                    page: pageNum
                }
            }).then((resp) => {
                this.loading = false;
                this.projects = resp.data.data.data;
                this.totPage = resp.data.data.last_page;
            });
        }
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
                <ProjectCard :project="project" />
            </div>
        </div>

        <nav aria-label="Result page for projects">
            <ul class="pagination justify-content-end">
                <li class="page-item" :class="{'disabled': curPage === 1}"><a class="page-link" href=""
                        @click.prevent="getProjectsPage(curPage - 1)"><i class="fa-solid fa-left-long"></i></a></li>
                <li v-for="page in totPage" class="page-item" :class="{'active': page === curPage}"><a class="page-link" href=""
                        @click.prevent="getProjectsPage(page)">{{ page }}</a></li>
                <li class="page-item" :class="{'disabled': curPage === totPage}"><a class="page-link" href="" @click.prevent="getProjectsPage(curPage + 1)"><i class="fa-solid fa-right-long"></i></a>
                </li>
            </ul>
        </nav>
    </div>
</template>

<style lang="scss" scoped></style>