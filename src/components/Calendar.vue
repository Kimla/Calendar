<template>
    <div class="Calendar">
        <h1>Calendar</h1>
        <div class="days">
            <div class="day" v-for="day in dayNames">{{ day }}</div>
        </div>
        <div class="days">
            <div class="day" v-for="day in days" :class="{ isActive: isToday(day) }">
                {{ getDate(day) }}
            </div>
        </div>
    </div>
</template>

<script>
import getMonth from 'date-fns/get_month';
import startOfMonth from 'date-fns/start_of_month';
import endOfMonth from 'date-fns/end_of_month';
import startOfWeek from 'date-fns/start_of_week';
import endOfWeek from 'date-fns/end_of_week';
import eachDay from 'date-fns/each_day';
import getDate from 'date-fns/get_date';
import isToday from 'date-fns/is_today';

export default {
    name: 'calendar',
    data() {
        return {
            dayNames: [
                'Monday',
                'Tuesday',
                'Wednesday',
                'Thursday',
                'Friday',
                'Saturday',
                'Sunday',
            ],
        };
    },
    computed: {
        month() {
            return getMonth(new Date());
        },
        startDay() {
            const firstInMonth = startOfMonth(new Date());
            return startOfWeek(firstInMonth, { weekStartsOn: 1 });
        },
        endDay() {
            const lastInMonth = endOfMonth(new Date());
            return endOfWeek(lastInMonth, { weekStartsOn: 1 });
        },
        days() {
            return eachDay(
                this.startDay,
                this.endDay,
            );
        },
    },
    methods: {
        isToday,
        getDate,
    },
};
</script>

<style lang="css">
.days {
    display: flex;
    flex-wrap: wrap;
}
.day {
    width: calc(100% / 7);
    text-align: center;
    padding: 30px;
    font-weight: bold;
    font-size: 18px;
}
.day.isActive {
    background-color: red;
    color: #fff;
}
</style>
