<script>
export default {
    props: {
        title: String,
        content: String,
    },
    data() {
        return {
            isDone: Boolean,
        }
    },
    methods: {
        deleteTask() {
            this.$emit('deleteTask')
        }
    }
}
</script>

<template>
    <div class="card mb-3">
        <div class="card-header d-flex">
            <span>{{ title }}</span>
            <button type="button" class="btn-close ms-auto" aria-label="Close" @click="deleteTask"></button>
        </div>
        <div class="card-body">
            <p class="content">{{ content }}</p>
        </div>
    </div>
</template>