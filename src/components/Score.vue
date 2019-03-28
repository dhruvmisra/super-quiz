<template>
    <div class="card mb-4 border-0">
        <div class="card-body row">
            <h5 class="card-text">Score: <span class="score">{{ score }}</span></h5>
            <transition name="add">
                <div v-if="added" class="score">+1</div>
            </transition>
            <h5 class="card-text ml-auto">High-score: <span class="score">{{ highScore }}</span></h5>
        </div>
    </div>
</template>

<script>    
    export default {
        props: ['score', 'highScore'],
        data() {
            return {
                added: false
            }
        },
        watch: {
            score(newValue, oldValue) {
                if(newValue > oldValue) {
                    this.added = true;
                    setTimeout(() => {
                        this.added = false;
                    }, 1000);
                }
            }
        }
    }
</script>

<style>
    .score {
        color: red;
    }
    .add-enter-active {
        animation: add 1s ease-in forwards;
    }
    .add-leave-active {
        opacity: 0;
    }
    @keyframes add {
        0% {
            opacity: 0;
            transform: translateX(0);
        } 
        50% {
            opacity: 1;
            transform: translateX(10px);
        }
        100% {
            opacity: 0;
            transform: translateX(20px);
        }
    }
</style>
