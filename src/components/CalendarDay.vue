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
            this.$emit('changeDay');
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
