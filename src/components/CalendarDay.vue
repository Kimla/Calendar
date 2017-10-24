<template>
    <div class="day" :class="{ isActive: day.active }" @click="clickHandler()">
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
</style>
