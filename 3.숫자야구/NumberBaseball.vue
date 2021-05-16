<template>
    <div>
        <h1>{{result}}</h1>
        <form @submit.prevent="onSubmitForm">
            <input ref="answer" minlength="3" maxlength="3" v-model="value" />
            <button type="submit">입력</button>
        </form>
        <div>남은 시도횟수 : {{remainTries}}</div>
        <div>시도 : {{tries.length}}</div>
        <ul>
            <li v-for="t in tries">
                <div>{{t.try}}</div>
                <div>{{t.result}}</div>
            </li>
        </ul>
    </div>
</template>

<script>
    const getNumbers = (num) => {
        const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9];
        const arr = [];
        for (let i = 0 ; i < num ; i++) {
            const chosen = numbers.splice(Math.floor(Math.random() * (9-i)), 1)[0];
            arr.push(chosen);
        }

        return arr;
    };

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
            onSubmitForm() {
                this.remainTries--;
                console.log(this.value);

                let strike = 0;
                let ball = 0;
                let out = 0;
                let result = '';

                if (this.value === this.answer.join('')) {
                    result = '홈런입니다...!!!';
                } else {
                    const valueArr = this.value.split('').map(v => parseInt(v));
                    for (let i = 0 ; i < this.answer.length ; i++) {
                        if(valueArr[i] === this.answer[i]) {
                            strike++;
                        } else if (this.answer.includes(valueArr[i])) {
                            ball++;
                        } else {
                            out++;
                        }
                    }

                    result = strike + 'S ' + ball + 'B ' + out + 'O';
                }

                this.tries.push({
                    try: this.value,
                    result : result
                });
                this.value = '';
                console.log(this.tries);
                this.$refs.answer.focus();
            }
        }
    }
</script>

<style>

</style>