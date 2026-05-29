<script>
import JobCard from './JobCard.vue'

export default {
    components: {
        JobCard
    },
    props: {
        jobs: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            searchQuery: '',
            selectedField: 'Все',
            showForm: false,
            newJob: {
                title: '',
                field: 'IT',
                salary: null,
                isInDemand: false,
                icon: 'https://flaticon.com',
                tagsString: ''
            }
        }
    },
    methods: {
        filterByField(field) {
            this.selectedField = field; 
        },
        resetFilters() {
            this.selectedField = 'Все';
            this.searchQuery = '';
        },
        addJob() {
            if (!this.newJob.title || !this.newJob.salary) {
                alert('Пожалуйста, заполните название и зарплату!');
                return;
            }
            const tags = this.newJob.tagsString
                ? this.newJob.tagsString.split(',').map(tag => tag.trim()).filter(Boolean)
                : [];

            const jobToAdd = {
                id: Date.now(), 
                title: this.newJob.title,
                field: this.newJob.field,
                salary: Number(this.newJob.salary),
                isInDemand: this.newJob.isInDemand,
                icon: this.newJob.icon,
                tags: tags
            };
            this.$emit('add-new-job', jobToAdd);
            this.newJob = {
                title: '',
                field: 'IT',
                salary: null,
                isInDemand: false,
                icon: 'https://flaticon.com',
                tagsString: ''
            };
            this.showForm = false;
        }
    },
    computed: {
        filteredJobs() {
            return this.jobs.filter(job => {
                const matchesSearch = job.title.toLowerCase().includes(this.searchQuery.toLowerCase());
                const matchesField = this.selectedField === 'Все' || job.field === this.selectedField;
                return matchesSearch && matchesField;
            });
        }
    }
}
</script>

<template>
  <div class="app-wrapper"> 
    <nav class="navbar navbar-dark bg-dark py-2 py-md-4 mb-4">
        <div class="container flex-column align-items-center text-center">
            <h1 class="navbar-brand m-0 mb-3 fs-3 fs-md-1 w-100 text-center">Атлас профессий</h1>
            <div class="w-100 d-flex justify-content-center justify-content-md-center">
                <div class="w-100" style="max-width: 500px; position: relative;">
                    <input 
                        v-model="searchQuery" 
                        type="text" 
                        placeholder="Поиск профессии по названию..." 
                        class="form-control rounded-pill pe-5"
                    />
                    <button 
                        v-if="searchQuery" 
                        @click="searchQuery = ''" 
                        class="btn btn-link text-secondary position-absolute end-0 top-50 translate-middle-y text-decoration-none"
                        style="z-index: 5;"
                    >
                        ✖
                    </button>
                </div>
            </div>

        </div>
    </nav>

    <div class="container mb-4 text-center">
        <button @click="showForm = !showForm" class="btn btn-success mb-4">
            {{ showForm ? '✖ Закрыть форму' : '➕ Добавить новую профессию' }}
        </button>
        <div v-if="showForm" class="card p-4 mx-auto text-start mb-4 bg-light shadow-sm" style="max-width: 600px;">
            <h4 class="mb-3 text-center">Новая профессия</h4>
            <form @submit.prevent="addJob">
                <div class="mb-3">
                    <label class="form-label">Название профессии *</label>
                    <input v-model="newJob.title" type="text" class="form-control" required placeholder="Например: Frontend-разработчик">
                </div>
                <div class="row">
                    <div class="col-md-6 mb-3">
                        <label class="form-label">Сфера деятельности</label>
                        <select v-model="newJob.field" class="form-select">
                            <option value="IT">IT</option>
                            <option value="Медицина">Медицина</option>
                            <option value="Безопасность">Безопасность</option>
                            <option value="Строительство">Строительство</option>
                            <option value="Медиа">Медиа</option>
                            <option value="Экология">Экология</option>
                            <option value="Лингвистика">Лингвистика</option>
                            <option value="Безопасность">Безопасность</option>
                            <option value="Медиа">Медиа</option>
                            <option value="Искусство">Искусство</option>
                        </select>
                    </div>
                    <div class="col-md-6 mb-3">
                        <label class="form-label">Зарплата (руб.) *</label>
                        <input v-model="newJob.salary" type="number" class="form-control" required placeholder="120000">
                    </div>
                </div>
                <div class="mb-3">
                    <label class="form-label">Теги (через запятую)</label>
                    <input v-model="newJob.tagsString" type="text" class="form-control" placeholder="Информатика, Математика">
                </div>
                <div class="mb-3 form-check">
                    <input v-model="newJob.isInDemand" type="checkbox" class="form-check-input" id="demandCheck">
                    <label class="form-check-label" for="demandCheck">Востребованная профессия</label>
                </div>
                <button type="submit" class="btn btn-primary w-100">Сохранить</button>
            </form>
        </div>
        <div class="d-flex flex-wrap justify-content-center gap-2">
            <button @click="filterByField('Все')" class="btn btn-outline-primary" :class="{ active: selectedField === 'Все' }">Все сферы</button>
            <button @click="filterByField('IT')" class="btn btn-outline-primary" :class="{ active: selectedField === 'IT' }">IT</button>
            <button @click="filterByField('Медицина')" class="btn btn-outline-primary" :class="{ active: selectedField === 'Медицина' }">Медицина</button>
            <button @click="filterByField('Строительство')" class="btn btn-outline-primary" :class="{ active: selectedField === 'Строительство' }">Строительство</button>
            <button @click="filterByField('Безопасность')" class="btn btn-outline-primary" :class="{ active: selectedField === 'Безопасность' }">Безопасность</button>
            <button @click="filterByField('Медиа')" class="btn btn-outline-primary" :class="{ active: selectedField === 'Медиа' }">Медиа</button>
            <button @click="filterByField('Искусство')" class="btn btn-outline-primary" :class="{ active: selectedField === 'Искусство' }">Искусство</button>
            <button @click="resetFilters" class="btn btn-secondary ms-md-3">🔄 Сбросить фильтры</button>
        </div>
    </div>

    <div class="container">
        <h2 class="mb-4 text-center">Профессии</h2>
        <div v-if="filteredJobs.length > 0" class="row g-4">
            <div 
                v-for="job in filteredJobs" 
                :key="job.id" 
                class="col-12 col-md-6 col-lg-4"
            >
                <JobCard :job="job" @delete="$emit('delete-job', job.id)" />
            </div>
        </div>
        <div v-else class="alert alert-danger text-center my-4" role="alert">
            🔍 Профессии по вашему запросу не найдены. Попробуйте ввести другое название.
        </div>
    </div>
  </div>
</template>

<style scoped>
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}
.navbar {
    background-color: #2c3e50 !important; 
}
</style>