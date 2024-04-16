<script>
export default {
    props: {
        tasks: Array,
    },
    emits: ['newTask'],
    data() {
        return {
            title: "",
            content: "",
        }
    },
    methods: {
        makeTask() {
            if (this.title == "" && this.content == "") return;
            this.$emit('newTask', this.title, this.content);
            this.title = "";
            this.content = "";
        }
    }
}
</script>

<template>
    <div class="card mb-3">
        <div class="card-header">TODO</div>
        <div class="card-body">
            <div class="mb-3">
                <label class="form-label">標題</label>
                <input type="text" class="form-control" id="taskTitle" placeholder="輸入標題" v-model="title">
            </div>
            <div class="mb-3">
                <label class="form-label">內文</label>
                <textarea class="form-control" id="taskContent" rows="2" placeholder="輸入內文"
                    v-model="content"></textarea>
            </div>
            <div>
                <button type="submit" class="btn btn-primary" @click="makeTask">
                    新增任務
                </button>
            </div>
        </div>
    </div>
</template>