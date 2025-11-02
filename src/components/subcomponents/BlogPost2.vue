<script>
    export default {
        // Add code if/as necessary
        // Hint: Add properties subject, entry and mood
        props: {
            id: [String, Number],
            subject: String, 
            entry: String, 
            mood: String 
        },
        computed: {
            imgLoc() {
                return `/assets/${this.mood.toLowerCase()}.png`
            }
        }
    }
</script>


<template>
    <!-- TODO: add your template code here. Use boostrap card --> 
    <div class="card mb-2" style="width: 18rem;">
        <img :src="imgLoc" class="card-img-top" alt="mood image">
        <div class="card-body">
        <h5 class="card-title mb-0">{{ subject }}</h5>
        </div>
        <p class="card-text mt-2">{{ entry }}</p>
        <div class="mt-2">
        <button
            type="button"
            class="btn btn-primary btn-sm"
            @click="$emit('delete-post', id)"  
        >
            Delete
        </button>
        </div>
    </div>
</template>

