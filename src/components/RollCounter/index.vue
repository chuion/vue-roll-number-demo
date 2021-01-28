<template>
    <div class="count">
        <RollNumber animate-name="first" :num="numberList[0]" :infinite-roll="infiniteRoll" />
        <RollNumber animate-name="second" :num="numberList[1]" :infinite-roll="infiniteRoll" />
        <RollNumber animate-name="third" :num="numberList[2]" :infinite-roll="infiniteRoll" />
    </div>
</template>

<script>
import RollNumber from './RollNumber'
export default {
    name: 'RollCounter',
    components: {
        RollNumber
    },
    data() {
        return {
            targetNum: '',
            infiniteRoll: false
        }
    },
    computed: {
        numberList() {
            if (!this.targetNum) {
                return ['', '', '']
            }
            const target = this.targetNum + '';
            const targetLen = target.length;
            const LEN = 3;
            let res = ''
            for (let i = 0; i < LEN - targetLen; i++) {
                res+='0'
            }
            res += target;
            return res.split('')
        }
    },
    watch: {
        targetNum(val) {
            if (val) {
                this.infiniteRoll = false;
            }
        }
    },
    mounted() {
        setTimeout(() => {
            this.targetNum = '106'
        }, 3000)
    }
    
}
</script>

<style lang="scss" scoped>
.count {
    display: flex;
}
</style>