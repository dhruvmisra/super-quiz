<template>
    <div class="container">
        <br>
        <h1 class="text-center">The Super Quiz</h1>
        <br>
        <hr>
        <app-score :score="score" :highScore="highScore"></app-score>
        <div class="col-sm-6 mx-auto">
            <transition name="flip" mode="out-in">
                <component :is="mode"
                            @answered="check"
                            @next="mode = 'app-question'">
                </component>
            </transition>
        </div>
    </div>
</template>

<script>
    import Question from './components/Question.vue';
    import Success from './components/Sucess.vue';
    import Score from './components/Score.vue';

    export default {
        components: {
            'app-question': Question,
            'app-success': Success,
            'app-score': Score,
        },
        data() {
            return {
                mode: 'app-question',
                animate: '',
                score: 0,
                highScore: 0
            };
        },
        methods: {
            check(isCorrect) {
                if(isCorrect) {
                    this.score++;
                    if(this.highScore < this.score) {
                        this.highScore = this.score;
                    }
                    this.mode = 'app-success';
                } else {
                    alert('Wrong answer, try again. Your Score: ' + this.score);
                    this.score = 0;
                }
            }
        }
    }
</script>

<style>
    .flip-enter-active {
        animation: scale-in 0.5s ease-out forwards;
    }
    .flip-leave-active {
        animation: move-down 0.25s ease-out forwards;
    }

    @keyframes flip-out {
        from {
            transform: rotateY(0deg);
        }
        to {
            transform: rotateY(90deg);
        }
    }
    @keyframes flip-in {
        from {
            transform: rotateY(90deg);
        }
        to {
            transform: rotateY(0deg);
        }
    }

    @keyframes scale-in {
        0% {
            transform: scale(0, 0);
        }
        60% {
            transform: scale(1.1, 1.1); 
        }
        100% {
            transform: scale(1, 1);
        }
    }

    @keyframes move-down {
        0% {
            transform: translateY(0);
        }
        100% {
            transform: translateY(50px);
            opacity: 0;
        }    
    }
</style>
