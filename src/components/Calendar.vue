<template>
    <div class="Calendar">
        <h1>Calendar</h1>
        <div class="days">
            <div class="day" v-for="day in dayNames">{{ day }}</div>
        </div>
        <div class="days">
            <CalendarDay v-for="day in days" :key="day.number" :day="day" @changeDay="changeActiveDay(day)"></CalendarDay>
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
import isSameDay from 'date-fns/is_same_day';
import CalendarDay from './CalendarDay';

export default {
    name: 'calendar',
    components: {
        CalendarDay,
    },
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
            activeDay: new Date(),
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
            const days = eachDay(
                this.startDay,
                this.endDay,
            );

            const out = [];

            for (let i = 0; i < days.length; i += 1) {
                const date = days[i];
                out.push({
                    date,
                    number: this.getDate(date),
                    active: this.isSameDay(date, this.activeDay),
                });
            }

            return out;
        },
    },
    methods: {
        changeActiveDay(day) {
            this.activeDay = day.date;
        },
        isToday,
        getDate,
        isSameDay,
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
