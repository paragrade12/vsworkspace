<template>
    <div>
        <div id="screen">{{}}</div>
        <div>
            <div>평균 시간 : {{}}</div>
            <button @click="onReset">리셋</button>
        </div>
    </div>
</template>

<script>

    export default {
        data() {
            return {
                answer: getNumbers(3),
                remainTries: 5,
                tries : [],
                value : '',
                result : '',
                isSuccess: false
            }
        },
        methods : {
            onReset() {
                
            }
        }
    }
</script>

<style>

</style>