<template>
    <div class="Calendar">
        <h1>Calendar</h1>
        {{ days }}
    </div>
</template>

<script>
import getMonth from 'date-fns/get_month';
import startOfMonth from 'date-fns/start_of_month';
import endOfMonth from 'date-fns/end_of_month';
import startOfWeek from 'date-fns/start_of_week';
import endOfWeek from 'date-fns/end_of_week';
import eachDay from 'date-fns/each_day';

export default {
    name: 'calendar',
    computed: {
        month() {
            return getMonth(new Date());
        },
        startDay() {
            const firstInMonth = startOfMonth(this.month);
            return startOfWeek(firstInMonth, { weekStartsOn: 1 });
        },
        endDay() {
            const lastInMonth = endOfMonth(this.month);
            return endOfWeek(lastInMonth, { weekStartsOn: 1 });
        },
        days() {
            return eachDay(
                this.startDay,
                this.endDay,
            );
        },
    },
};
</script>

<style lang="css">
</style>
