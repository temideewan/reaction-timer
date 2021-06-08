<template>
    <div>
        <p>Your score is {{score}} ms</p>
        <p class="rank">{{rank}}</p>
    </div>
</template>

<script>
    export default {
        name: 'Results',
        props:['score'],
        data(){
            return {
                rank: null
            }
        },

        mounted(){
            if(this.score < 250){
                this.rank = 'ninja fingers';
            } else if( this.score < 400){
                this.rank = 'Rapid reflexes';
                
            } else{
                this.rank = 'Snail pace';

            }
        }
    }
</script>

<style>
.rank{
    font-size: 1.4rem;
    font-weight: bold;
    color: #0faf87;
}
</style>