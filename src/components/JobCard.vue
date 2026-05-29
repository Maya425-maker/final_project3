<script>
export default {
    props: {
        job: {
            type: Object,
            required: true
        }
    }
}
</script>

<template>
    <div class="card h-100 shadow-sm">
        <button @click="$emit('delete')" class="btn btn-sm btn-danger position-absolute end-0 top-0 m-2" style="z-index: 2;" >
        🗑️
        </button>
        <div class="card-body p-4">
            <img :src="job.icon" alt="Иконка" class="img-fluid mb-3" style="width: 40px; height: 40px;" />
            
            <h3 class="card-title h5 mb-2 text-start">{{ job.title }}</h3>
            <p class="card-text text-success fw-bold mb-2">💰 {{ job.salary }} ₽</p>
            <p class="card-text text-muted small mb-3">Сфера: {{ job.field }}</p>
            <span v-if="job.isInDemand" class="badge bg-danger mb-3 d-inline-block">🔥 Востребованная</span>
            <div class="d-flex flex-wrap gap-2 mt-2">
                <span v-for="tag in job.tags" :key="tag" class="badge bg-light text-primary border">
                    {{ tag }}
                </span>
            </div>
        </div>
    </div>
</template>

<style scoped>
.job-card {
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    padding: 20px;
    background-color: #f9f9f9;
    box-shadow: 0 2px 4px rgba(0,0,0,0.05);
    position: relative;
}
.job-icon {
    width: 90px;
    height: 90px;
    margin-bottom: 10px;
}
.salary {
    font-weight: bold;
    color: #27ae60;
    margin: 5px 0;
}
.field {
    font-size: 14px;
    color: #7f8c8d;
}
.demand-badge {
    font-size: 12px;
    color: #e74c3c;
    font-weight: bold;
    margin-top: 5px;
}
.tags {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-top: 10px;
}
.tag {
    background-color: #e1f5fe;
    color: #0288d1;
    padding: 4px 8px;
    border-radius: 4px;
    font-size: 12px;
}
</style> 