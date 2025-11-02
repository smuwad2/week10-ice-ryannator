<script>
export default {
  props: {
    task: Object,
    idx: Number
  }
}
</script>

<template>
    <!-- TODO: add your template code here -->
    <div class="card mb-2" style="width: 22rem;">
        <div class="card-body">

        <div>Deadline: {{ task.deadline }}</div>

        <p class="card-text mt-2">{{ task.desc }}</p>

        <button
            class="btn btn-outline-success btn-sm"
            @click="$emit('delete-task', idx)"
        >
            Done
        </button>
        </div>
    </div>
</template>
