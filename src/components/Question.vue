<template>
    <div class="card text-center">
        <div class="card-header">
            {{ question }}
        </div>
        <div class="card-body">
            <button class="btn btn-primary btn-lg"
                    style="margin: 10px"
                    v-for="(option, index) in options"
                    :key="index"
                    @click="onAnswer(option.correct)">
                {{ option.answer }}
            </button>
        </div>
    </div>
</template>

<script>
    const ADDITION = 1;
    const SUBTRACTION = 2; 
    export default {
        data() {
            return {
                question: '',
                options: [
                    {answer: 0, correct: true},
                    {answer: 0, correct: false},
                    {answer: 0, correct: false},
                    {answer: 0, correct: false}
                ]
            };
        },
        created() {
                this.generateQuestion();
        },
        methods: {
            generateQuestion() {
                console.log('Generating Question');
                const firstNumber = this.generateRandom(1, 100);
                const secondNumber = this.generateRandom(1, 100);
                const operatorNumber = this.generateRandom(1, 2);

                let correctAnswer = 0;

                switch(operatorNumber) {
                    case ADDITION:
                        correctAnswer = firstNumber + secondNumber;
                        this.question = `What's ${firstNumber} + ${secondNumber}?`;
                        break;
                    case SUBTRACTION:
                        correctAnswer = firstNumber - secondNumber;
                        this.question = `What's ${firstNumber} - ${secondNumber}?`;
                        break;
                    default:
                        this.question = 'Oops, an error occurred';
                }
                for(let i = 0; i < 4; i++) {
                    this.options[i].answer = this.generateRandom(correctAnswer - 10, correctAnswer + 10, correctAnswer);
                    this.options[i].correct = false;
                }

                const correctOption = this.generateRandom(0, 3);
                this.options[correctOption].answer = correctAnswer;
                this.options[correctOption].correct = true;
            },
            generateRandom(min, max, except) {
                const rnd = Math.floor((Math.random()*max) + min);
                if(rnd == except) {
                    return this.generateRandom(min, max, except);
                }
                return rnd;
            },
            onAnswer(isCorrect) {
                this.$emit('answered', isCorrect);
            }
        }
    }
</script>

<style>
</style>
