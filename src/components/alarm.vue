<template>
    <ButtonAlarm v-bind:alarms="alarms" v-bind:hours="hours" v-bind:minutes="minutes" v-bind:seconds="seconds" v-bind:day="day" v-bind:dates="dates" v-bind:month="month" v-bind:years="years"/>
    <div class="date">
        <select id="date" ref="date">
            <option value="">date</option> 
            <option v-for="i in 31" v-bind:value="i"> {{ i }} </option>
        </select> -
        <select id="month" ref="month">
            <option value="">month</option>
            <option v-for="i in 12" v-bind:value="i"> {{ i }} </option>
        </select>
    </div>
    <div class="input">
        <select id="hour" ref="hour">
            <option v-for="i in 24" v-bind:value="i-1"> {{ ("0" + (i - 1)).slice(-2) }} </option>
        </select> :
        <select id="minute" ref="minute">
            <option v-for="i in 60" v-bind:value="i-1"> {{ ("0" + (i - 1)).slice(-2) }} </option>
        </select>
        <input type="text" v-model="this.msg">
        <select id="sound" ref="sound">
            <option value="alarm1.mp3">Sound 1</option>
            <option value="alarm2.mp3">Sound 2</option>
            <!-- <option value="sound3">Sound 3</option> -->
        </select>
        <div class="dayz">
            <input type="checkbox" ref="sun"> <label>Sun</label>
            <input type="checkbox" ref="mon"> <label>Mon</label>
            <input type="checkbox" ref="tue"> <label>Tue</label>
            <input type="checkbox" ref="wed"> <label>Wed</label>
            <input type="checkbox" ref="thu"> <label>Thu</label>
            <input type="checkbox" ref="fri"> <label>Fri</label>
            <input type="checkbox" ref="sat"> <label>Sat</label>
        </div>
    </div>
    <button @click="setAlarm()">Set Alarm</button>
    <ul class="alarms">
        <li v-for="(alarm,i) in alarms">
            <p> <span v-if="alarm.days.sun">Sun </span>
                <span v-if="alarm.days.mon">Mon </span>
                <span v-if="alarm.days.tue">Tue </span>
                <span v-if="alarm.days.wed">wed </span>
                <span v-if="alarm.days.thu">Thu </span>
                <span v-if="alarm.days.fri">Fri </span>
                <span v-if="alarm.days.sat">Sat </span>
                <span v-if="alarm.date != ''"> {{ alarm.date }} - {{ alarm.month }} || </span>
                {{ ("0" + alarm.hour).slice(-2)  }} : {{ ("0" + alarm.minute).slice(-2) }} 
                {{alarm.msg}} {{ alarm.sound }}
                <button @click="removeAlarm(i)">remove</button></p>
        </li>
    </ul>
</template>
<script>
import ButtonAlarm from './buttonAlarm.vue'
export default {
    name: "Alarm",
    props: ["hours", "minutes", "seconds", "day", "dates", "month", "years"],
    data() {
        return {
            alarms: [],
            msg: null
        };
    },
    methods: {
        setAlarm() {
            var newAlarm = {
                date: this.$refs.date.value,
                month: this.$refs.month.value,
                hour: parseInt(this.$refs.hour.value),
                minute: parseInt(this.$refs.minute.value),
                msg: this.msg,
                sound: this.$refs.sound.value,
                days:{
                    sun: this.$refs.sun.checked ? true : false,
                    mon: this.$refs.mon.checked ? true : false,
                    tue: this.$refs.tue.checked ? true : false,
                    wed: this.$refs.wed.checked ? true : false,
                    thu: this.$refs.thu.checked ? true : false,
                    fri: this.$refs.fri.checked ? true : false,
                    sat: this.$refs.sat.checked ? true : false
                }
            };
            this.alarms.push(newAlarm)
            console.log(this.alarms)
        },
        removeAlarm(i) {
            this.alarms.splice(i, 1)
        }
    },
    components: { ButtonAlarm }
}
</script>
<style>
.input, .alarms, .date{
    color: antiquewhite;
    font-size: 30px;
}
.date select{
    width: 70px;
}

select {
    width: 40px;
    height: 30px;
    margin: 10px;
}
button {
    height: 30px;
}
.alarms{
    border: 1px solid black;
    box-shadow: 1px 1px 2px grey
}
#sound{
    width: 80px;
}
</style>