<template>
    <div class="card bg-success text-white text-center">
        <div class="card-body">
            <h1>That's correct!</h1>
            <hr>
            <button class="btn btn-light text-success"
                    @click="next">
                Next Question
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        methods: {
            next() {
                this.$emit('next');
            }
        }
    }
</script>

<style>
</style>
