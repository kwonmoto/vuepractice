<template>
    <div class="oneroom">
        <img :src="row.image" class="room-img"/>
        <!-- <h4 @click="modalShow(true); nowNum(i)">{{ row.title }}</h4> -->
        <h4 @click="modalToggleOn()">{{ row.title }}</h4>
        <p>{{ row.price }}원</p>
     </div>
</template>

<script>
export default {
    name: "DetailCard",
    props: {
        row: Object,
    },
    methods: {
        modalToggleOn() {
            this.$emit('openModal', this.row.id)
        },
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
