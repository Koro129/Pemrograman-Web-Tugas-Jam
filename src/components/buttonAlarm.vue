<template>
<div v-show="value1" ref="box" class="boxAlarm">
    <div class="clock">{{ hourss }} : {{ minutess }} - {{ msgg }} </div>
    <button @click="stopAlarm()">Stop Alarm</button>
    <button @click="snooze()">Snooze</button>
</div>
</template>
<script>

export default {
    name: 'buttonAlarm',
    props: ["alarms", "hours", "minutes", "seconds", "day", "dates", "month", "years"],
    data(){
        return {
            hourss: null,
            minutess: null,
            msgg: null,
            value1: false,
            music: null
        }
    },
    methods: {
        vis() {
            for(var i = 0; i < this.alarms.length; i++){
                if(this.alarms[i].date == '' && this.alarms[i].hour == this.hours && this.alarms[i].minute == this.minutes && this.seconds == 0){
                    if(this.day == 'Sun' && this.alarms[i].days.sun == true) this.play(i)
                    else if(this.day == 'Mon' && this.alarms[i].days.mon == true) this.play(i)
                    else if(this.day == 'Tue' && this.alarms[i].days.tue == true) this.play(i)
                    else if(this.day == 'Wed' && this.alarms[i].days.wed == true) this.play(i)
                    else if(this.day == 'Thu' && this.alarms[i].days.thu == true) this.play(i)
                    else if(this.day == 'Fri' && this.alarms[i].days.fri == true) this.play(i)
                    else if(this.day == 'Sat' && this.alarms[i].days.sat == true) this.play(i)
                    else if(this.alarms[i].days.sun == false && this.alarms[i].days.mon == false && this.alarms[i].days.tue == false 
                            && this.alarms[i].days.wed == false && this.alarms[i].days.thu == false
                            && this.alarms[i].days.fri == false && this.alarms[i].days.sat == false) this.play(i)
                }
                else if(this.alarms[i].date == this.dates && this.alarms[i].month == this.month && this.alarms[i].hour == this.hours && this.alarms[i].minute == this.minutes && this.seconds == 0){
                    this.play(i)
                }
            }
        },
        play(i){
            this.hourss = this.alarms[i].hour <= 9 ? "0" + this.alarms[i].hour : this.alarms[i].hour
            this.minutess = this.alarms[i].minute <= 9 ? "0" + this.alarms[i].minute : this.alarms[i].minute
            this.msgg = this.alarms[i].msg
            this.value1 = true
            this.music = new Audio(this.alarms[i].sound)
            this.music.play()
            console.log(this.music)    
        },
        stopAlarm(){
            this.value1 = false
            this.music.pause()
            this.music.currentTime=0
        },
        snooze(){
            this.stopAlarm()
            for(var i = 0; i < this.alarms.length; i++){
                if(this.alarms[i].date == '' && this.alarms[i].hour == this.hours && this.alarms[i].minute == this.minutes){
                    if(this.alarms[i].minute < 55) this.alarms[i].minute += 5
                    else{
                        this.alarms[i].minute = (this.alarms[i].minute + 5) - 60
                        this.alarms[i].hour += 1
                        this.music = new Audio(this.alarms[i].sound)
                    }
                }
                else if(this.alarms[i].date == this.dates && this.alarms[i].month == this.month && this.alarms[i].hour == this.hours && this.alarms[i].minute == this.minutes){
                    if(this.alarms[i].minute < 55) this.alarms[i].minute += 5
                    else{
                        this.alarms[i].minute = (this.alarms[i].minute + 5) - 60
                        this.alarms[i].hour += 1
                        this.music = new Audio(this.alarms[i].sound)
                    }
                }
            }

        }
    },
    mounted() {
        setInterval(this.vis, 1000)
    }
}
</script>
<style>
.boxAlarm{
    color: antiquewhite;
    padding: 5px;
    border-radius: 10px;
    background: red;
    box-shadow: 1px 1px 1px grey;
}
</style>