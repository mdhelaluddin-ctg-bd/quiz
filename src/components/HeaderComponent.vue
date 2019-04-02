<template>
    <div>
        <b-nav tabs>
            <b-nav-item disabled>Quiz</b-nav-item>
            <b-nav-item>Question : {{ currentQuestion }} / {{ totalQuestion }}</b-nav-item>
            <b-nav-item>
                <span class="text-danger">
                    <strong>Result : {{ noOfCorrectAnswer }} / {{ totalQuestion }}</strong>
                </span>
            </b-nav-item>            
        </b-nav>
    </div>
</template>

<script>
export default {
    props : {
        totalQuestion : Number,
        currentQuestion: Number,
        noOfCorrectAnswer: Number
    }
}
</script>
