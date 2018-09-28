<template>
    <span id="time" v-html="time"></span>
</template>

<style>
    
</style>

<script>
export default {
    name: 'StopWatch',
    data() {
        return {
            state: "started",
            startTime: Date.now(),
            currentTime: Date.now(),
            interval: null,
            periodTaken: ''
        }
    },

    mounted() {
        this.interval = setInterval(this.updateCurrentTime, 1000);
    },

    destroyed() {
        this.periodTaken = this.time;
        console.log(this.periodTaken)
        clearInterval(this.interval)
    },

    computed: {
        time() {
            return this.hours + ':' + this.minutes + ':' + this.seconds;
        },
        milliseconds() {
            return this.currentTime - this.$data.startTime;
        },
        hours() {
            var lapsed = this.milliseconds;
            var hrs = Math.floor((lapsed / 1000 / 60 / 60));
            return hrs >= 10 ? hrs : '0' + hrs;
        },
        minutes() {
            var lapsed = this.milliseconds;
            var min = Math.floor((lapsed / 1000 / 60) % 60);
            return min >= 10 ? min : '0' + min;
        },
        seconds() {
            var lapsed = this.milliseconds;
            var sec = Math.ceil((lapsed / 1000) % 60);
            return sec >= 10 ? sec : '0' + sec;
        }
    },
    methods: {
        reset() {
            this.$data.state = "started";
            this.$data.startTime = Date.now();
            this.$data.currentTime = Date.now();
        },
        pause() {
            this.$data.state = "paused";
        },
        resume() {
            this.$data.state = "started";
        },
        updateCurrentTime() {
            if (this.$data.state == "started") {
                this.currentTime = Date.now();
            }
        }        
    }
} 
</script>