<template>
    <div class="reuslt">
        <div class="title">{{ results[resultIndex].title }}</div>
        <div class="desc"> {{ results[resultIndex].desc }} </div>
    </div>
</template>

<script>
export default {
    props:{
        correctAnswers: Number,
        results: Array
    },
    computed:{
        resultIndex(){
            let index = 0

            this.results.forEach( (e, i) => {
                if(e.min <= this.correctAnswers && e.max >= this.correctAnswers){
                    index = i
                }
            } )

            return index
        }
    }
}    
</script>

<style>

</style>