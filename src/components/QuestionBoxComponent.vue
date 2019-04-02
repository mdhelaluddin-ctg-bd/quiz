<template>
    <div>
        <br />
         <b-row>
            <b-col offset="3" sm="6">
                <b-jumbotron>
                    <template slot="lead">
                        <span v-html="currentQuestion.question"></span>
                    </template>

                    <hr class="my-4" />

                    <b-form-group label="Individual radios">
                        <b-form-radio 
                            v-for="(answer, index) in answers" 
                            :key="index" 
                            :value="answer" 
                            v-model="selected" 
                            :class="{
                                'text-success': isSubmitted && answer === currentQuestion.correct_answer, 
                                'text-danger': isSubmitted && selected === answer && selected !== currentQuestion.correct_answer
                            }" name="some-radios">
                            <span v-html="answer"></span>
                        </b-form-radio>
                    </b-form-group>
                    <hr>

                    <b-button :disabled="isSubmitted || selected.length <= 0" variant="primary" v-on:click.prevent.self="submitAnswer()">Submit</b-button>
                    &nbsp;
                    <b-button v-if="index < totalQuestion" :disabled="!isSubmitted" variant="success" @click="next" >Next &gt;</b-button>
                    &nbsp;
                    <b-button v-if="totalQuestion === index && isSubmitted" variant="primary" @click="startNewQuiz" >Start a new Quiz !</b-button>
                    
                </b-jumbotron>
            </b-col>
        </b-row>    
    </div>
</template>

<script>
export default {
    name: 'QuestionBoxComponent',
    props: {
        'currentQuestion' : Object, 
        'totalQuestion' : Number,
        'index' : Number,
        'next' : Function,
        'increaseCorrectAnswer' : Function,
        'startNewQuiz' : Function
    },
    data () {
        return {
            selected : '',
            isSubmitted : false
        }
    },
    methods: {
        submitAnswer() {
            this.isSubmitted = true;
            if(this.currentQuestion.correct_answer === this.selected) {
                this.increaseCorrectAnswer()
            }
        }
    },
    mounted : function() {
        //this.increaseCorrectAnswer()
    },
    computed : {
        classObject: function () {
            return {
                'text-success': this.isSubmitted && this.selected === this.currentQuestion.correct_answer
            }
        },
        answers() {
            let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
            answers.sort(() => Math.random() - 0.5);
            
            return answers;
        }
    },
    watch : {
        currentQuestion: function() {
            this.selected = '';
            this.isSubmitted = false;
        }
    }
}
</script>
