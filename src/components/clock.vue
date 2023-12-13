<template>
    <div class="boxClock">
        <div class="date">{{day}}, {{ dates }} - {{ month }} - {{ years }}</div>
        <div class="clock">{{ hourss }} : {{ minutess }} : {{ seconds }}</div>
    </div>
    <Alarm v-bind:hours="hours" v-bind:minutes="minutes" v-bind:seconds="seconds" v-bind:day="day" v-bind:dates="dates" v-bind:month="month" v-bind:years="years"/>
</template>

<script>
import Alarm from './alarm.vue';
    export default {
    name: "Clock",
    data() {
        return {
            days:['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
            day: null,
            dates:null,
            month: null,
            years: null,
            hours: null,
            minutes: null,
            seconds: null,
            hourss: null,
            minutess: null
        };
    },
    methods: {
        setDateTime() {
            const date = new Date();
            this.day = this.days[date.getDay()],
            this.dates = date.getDate(),
            this.month = date.getMonth() + 1,
            this.years = date.getFullYear(),
            this.hours = date.getHours(),
            this.minutes = date.getMinutes(),
            this.seconds = date.getSeconds(),
            this.hourss = this.hours <= 9 ? "0" + this.hours : this.hours,
            this.minutess = this.minutes <= 9 ? "0" + this.minutes : this.minutes,
            this.seconds = this.seconds <= 9 ? "0" + this.seconds : this.seconds;
        }
    },
    mounted() {
        this.setDateTime
        setInterval(this.setDateTime, 1000);
    },
    components: { Alarm }
}
</script>
<style>
.boxClock{
    color: antiquewhite;
    padding: 10px;
}
.date{
    font-size: 30px;
}
.clock{
    font-size: 50px;
}
</style>