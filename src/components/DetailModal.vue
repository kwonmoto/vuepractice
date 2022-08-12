<template>
    <div v-if="modalToggle" class="black-bg">
        <div class="white-bg">
        <img :src="oneroom[oneroomNum].image" class="room-img"/>
        <h4>{{ oneroom[oneroomNum].title }}</h4>
        <p>{{ oneroom[oneroomNum].content }}</p>
        <!-- <input @input="changeMonth($event)"/> -->
        <input v-model="month" type="number" min="1"/>
        <p>{{month}}개월 선택함: {{ oneroom[oneroomNum].price * month }}원</p>
        <button @click="modalToggleOff()" >닫기</button>
        </div>
    </div>
</template>

<script>

export default {
    name: "DetailModal",
    data(){
        return {
            month: 3
            }
    },
    props: {
        oneroom: Array,
        oneroomNum: Number,
        modalToggle: Boolean,
    },
    updated() {
        if (this.month <= 2) {
            alert('3개월 이상부터 입력 가능합니다.');
            this.month = 3;
        }
        if (isNaN(this.month)) {
            alert('숫자를 입력하세요.')
            this.month = 1;
        }
    },
    methods: {
        modalToggleOff() {
            this.$emit('closeModal');
        },
        // changeMonth(e) {
        //     this.month = e.target.value;
        // }
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
