<template>
  <div>
    <div>
      <h1>Счётчик</h1>
    </div>
    <div>
      <button @click="setMinute(1,0)">1 min</button>
      <button @click="setMinute(5,0)">5 min</button>
      <button @click="setMinute(15,0)">15 min</button>
      <button @click="setMinute(20,0)">20 min</button>
      <button @click="setMinute(30,0)">30 min</button>
      <button @click="setMinute(0,1)">1 hour</button>
      <br>
      <br>
      <button @click="setMinute">Your time:</button><input placeholder="Input your time">
      <br>
      <br>
      <button @click="stopTimer">Stop timer</button>
      <button @click="cleanTimer">Clean timer</button>
      <button @click="continueTimer">Continue timer</button>
      
    </div>
    <h1>{{ hourTime }}:{{ minuteTime }}:{{ secondTime }}</h1>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      hourTime:"00",
      minuteTime: "00",
      secondTime: "00",
      timer: null,
    };
  },
  methods: {
    setMinute(minute,hour) {  //по идее наоборот
      //const second = 1000
      //const minute = second * 60
      //const hour = minute * 60
      //const day = hour * 24

      let time = new Date(0, 0, 0, hour, minute, 0, 0);
      this.timer = setInterval(() => {
        this.secondTime = time.getSeconds();
        this.minuteTime = time.getMinutes();
        this.hourTime = time.getHours();
        time.setTime(time.getTime() - 1000);

        if (this.hourTime == 0 && this.minuteTime == 0 && this.secondTime == 0) { 
          let result = (hour == 0)  ? ' минут':' час'  //синтаксические ошибки по обработке данных
          let resultTime = (hour == 0) ? minute : hour

          alert("Прошло "+ resultTime  + result);
          this.stopTimer()
        }
      }, 1000);
    },

    stopTimer() {
      clearInterval(this.timer);
      clearTimeout(this.timer);
    },
    cleanTimer(){
      this.hourTime = '00'
      this.minuteTime ='00'
      this.secondTime = '00'
    },
    continueTimer(){  
      
    },
    
  },
};
</script>

<style>
</style>
