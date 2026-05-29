<script>
import JobList from './JobList.vue' 

export default {
    components: {
        JobList
    },
    data() {
        return {
            jobs: [
                { id: 1, title: 'Разработчик ИИ', field: 'IT', salary: 150000, isInDemand: true, icon: 'src/assets/ai_dev.png', tags: ['Информатика', 'Математика'] },
                { id: 2, title: 'Биоинженер', field: 'Медицина', salary: 90000, isInDemand: true, icon: 'src/assets/bioengineer.jpg', tags: ['Биология', 'Химия'] },
                { id: 3, title: 'Специалист по кибербезопасности', field: 'Безопасность', salary: 120000, isInDemand: true, icon: 'src/assets/cyber_sec.jpg', tags: ['Информатика'] },
                { id: 4, title: 'Архитектор умных домов', field: 'Строительство', salary: 100000, isInDemand: true, icon: 'src/assets/smart-house.jpg', tags: ['Физика', 'Информатика'] },
                { id: 5, title: 'Режиссер VR', field: 'Медиа', salary: 80000, isInDemand: false, icon: 'src/assets/vr.jpg', tags: ['Литература', 'Информатика'] },
                { id: 6, title: 'Инженер энергетики', field: 'Экология', salary: 95000, isInDemand: true, icon: 'src/assets/engineer.jpg', tags: ['Физика', 'География'] },
                { id: 7, title: 'Цифровой лингвист', field: 'Лингвистика', salary: 85000, isInDemand: false, icon: 'src/assets/linguist.jpg', tags: ['Русский язык', 'Информатика'] },
                { id: 8, title: 'Концепт-художник', field: 'Медиа', salary: 85000, isInDemand: true, icon: 'src/assets/artist.png', tags: ['Изобразительное искусство', 'История'] },
                { id: 9, title: 'Композитор видеоигр', field: 'Медиа', salary: 70000, isInDemand: false, icon: 'src/assets/composer.png', tags: ['Музыка', 'Информатика'] },
                { id: 10, title: 'Фотограф старинных интерьеров', field: 'Искусство', salary: 50000, isInDemand: false, icon: 'src/assets/photo.jpg', tags: ['Изобразительное искусство', 'История'] },
                { id: 11, title: 'Сценарист диалогов чат-ботов', field: 'Лингвистика', salary: 75000, isInDemand: true, icon: 'src/assets/screenwriter.png', tags: ['Русский язык', 'Литература'] },
                { id: 12, title: 'Криптоаналитик', field: 'IT', salary: 180000, isInDemand: true, icon: 'src/assets/crypto.jpg', tags: ['Математика', 'Информатика'] },
                { id: 13, title: 'Эко-аудитор', field: 'Экология', salary: 90000, isInDemand: false, icon: 'src/assets/eco.png', tags: ['Биология', 'География'] },
                { id: 14, title: 'Реставратор книг', field: 'Искусство', salary: 55000, isInDemand: false, icon: 'src/assets/book.jpg', tags: ['История', 'Химия'] },
                { id: 15, title: '3D-моделлер одежды', field: 'Медиа', salary: 110000, isInDemand: true, icon: 'src/assets/designer.jpg', tags: ['Изобразительное искусство', 'Информатика'] }
            ]
        }
    },
    methods: {
        handleAddNewJob(newJob) {
            this.jobs.push(newJob); 
        },
        handleDeleteJob(jobId) {
            const index = this.jobs.findIndex(job => job.id === jobId);
            if (index !== -1) {
                this.jobs.splice(index, 1);
            }
        }
    }
}
</script>

<template>
    <JobList :jobs="jobs" @add-new-job="handleAddNewJob" @delete-job="handleDeleteJob" /> 
</template>