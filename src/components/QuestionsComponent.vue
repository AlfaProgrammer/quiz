<template>
    <div class="questions-ctr">

        <div class="progress">
            <div class="bar" :style="{ width:`${questionsAnswered / questions.length * 100}%` }"></div>
            <div class="status"> {{questionsAnswered}} out of {{questions.length}} questions answered </div>
        </div>

        <transition-group name="fade">
            <div class="single-question"
                v-for="(question, index) in questions" :key="index"
                v-show="questionsAnswered === index"
            >
                <div class="question"> {{question.q}} </div>
                <div class="answers">
                    <div class="answer"
                        v-for="(answer, index) in question.answers" :key="index"
                        @click="answerChoosed(answer.is_correct)"
                    >
                        {{answer.text}}
                    </div>
                </div>
            </div>
        </transition-group>

    </div> 
</template>

<script>
export default {
    props:{
        questions:{
            type: Array,
            required: true
        },
        questionsAnswered: Number
    },
    emits:['verify-answer'],
    methods: {
        answerChoosed(is_correct){
            console.log(is_correct)
            this.$emit('verify-answer', is_correct)
        }
    },
    
}
</script>