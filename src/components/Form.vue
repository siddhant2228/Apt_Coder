<script setup>
    const props = defineProps(['registerTask', 'tempTask', 'changeFilter', 'editTempTask'])
</script>

<template>
    <form @submit.prevent="props.registerTask">
        <div class="row">
            <div class="col">
                <input :value="props.tempTask" @change="props.editTempTask" required
                    type="text" placeholder="Enter task description here" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Register</button>
            </div>
            <div class="col-md-2">
                <select @change="props.changeFilter" class="form-control">
                    <option value="all">All tasks</option>
                    <option value="pending">Pending</option>
                    <option value="completed">Completed</option>
                </select>
            </div>
        </div>
    </form>
</template>
