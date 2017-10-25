<template>
    <div class="day" :class="[{ isActive: day.active }, { isInCurrentMonth: day.isInCurrentMonth }]" @click="clickHandler()">
        {{ day.number }}
    </div>
</template>

<script>
export default {
    name: 'calendarDay',
    props: ['day'],
    methods: {
        clickHandler() {
            if (this.day.active) {
                return;
            }
            this.$emit('changeDay', this.day.number);
        },
    },
};
</script>

<style lang="css">
.day {
    background-color: #ddd;
}
.day.isInCurrentMonth {
    background-color: #fff;
}
.day.isActive {
    background-color: red;
    color: #fff;
}
</style>
