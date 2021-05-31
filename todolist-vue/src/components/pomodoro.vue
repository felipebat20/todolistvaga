<template>
	<div class="container">
		<nav>
			<ul class="menu-pomodoro">
				<li><a href="#" class="links-menu">Pomodoro</a></li>
				<li><a href="#" class="links-menu">Short Break</a></li>
				<li><a href="#" class="links-menu">Long Break</a></li>
			</ul>
		</nav>
		<div>
			<h1 class="time">{{ displayMinutes }}:{{ displaySeconds }}</h1>
		</div>
		<div class="button-pomodoro">
			<button class="start" @click="start">Start</button>
			<button class="stop" @click="stop">Stop</button>
			<button class="reset" @click="reset(timers[currentTimer].minutes)">Reset</button>
		</div>
	</div>
</template>

<script>
export default {
	components: {},
	props: {},
	data() {
		return {
			isRuning: false,
			timerInstace: null,
			totalSeconds: 25 * 60,
			currentTimer: 0,
			timers: [
				{
					name: "Pomodoro",
                    minutes: 25
				},
			],
		};
	},
	computed: {
		displayMinutes() {
			const minutes = Math.floor(this.totalSeconds / 60);
			return this.formatTime(minutes);
		},
		displaySeconds() {
			const seconds = this.totalSeconds % 60;
			return this.formatTime(seconds);
		},
	},
	methods: {
		formatTime(time) {
			if (time < 10) {
				return "0" + time;
			}
			return time.toString();
		},
		start() {
            this.stop();
            this.isRuning = true;
            if(this.totalSeconds <=0 ){
                this.stop();
                return
            }
            this.timerInstace = setInterval(() => {
               
                this.totalSeconds -= 1
            }, 1000)
		},
		stop() {
            this.isRuning = false;
            clearInterval(this.timerInstace);
        },
        reset(minutes){
            console.log(minutes)
            this.stop();
            this.totalSeconds = minutes * 60;
        }
	},
};
</script>

<style scoped>
    h1.time {
        font-size: 95px;
        font-family: Helvetica Neue, Helvetica, Arial, sans-serif;
        color: #222222;
        font-weight: bold;
        font-style: normal;
        line-height: 1.1;
        margin: 14px auto;
    }
    .container {
        background: white;
        width: 60%;
        margin: auto;
    }
    .menu-pomodoro li {
        display: inline-block;
        padding: 0.5em 4em;
        background-color: #2784a1;
        border: 1px solid black;
        border-collapse: collapse;
    }
    .menu-pomodoro li:nth-child(2) {
        border-right: transparent;
        border-left: transparent;
    }
    .menu-pomodoro li a.links-menu {
        text-decoration: none;
        font-weight: 700;
        font-family: Arial;
        color: white;
    }

    .button-pomodoro button {
        border: 1px solid black;
        border-radius: 0.2em;
        padding: 1em 1.8em;
        font-family: Arial, sans-serif;
        font-weight: 700;
        font-size: 1em;
        margin: 2% 5%;
        cursor: pointer;
    }
    .start {
        background-color: #5da423;
        border: 1px solid #396516;
        transition: all 0.2s linear;
        color: white;
    }
    .start:hover {
        background-color: #457a1a;
    }
    .stop {
        background: #c60f13;
        border: 1px solid #7f0a0c;
        color: white;
        transition: all 0.2s linear;
    }
    .stop:hover {
        background: #970b0e;
    }
</style>