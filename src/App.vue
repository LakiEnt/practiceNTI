<template>
  <div>
    <div class="btns">
      <h1 style="font-family: Roboto, sans-serif;">Счётчик</h1>
    </div>
      <div>
      <button class="btn" @click="setMinute(5, 0)">5 min</button>
      <button class="btn" @click="setMinute(1, 0)">1 min</button>
      <button class="btn" @click="setMinute(15, 0)">15 min</button>
      <button class="btn" @click="setMinute(20, 0)">20 min</button>
      <button class="btn" @click="setMinute(30, 0)">30 min</button>
      <button class="btn" @click="setMinute(0, 1)">1 hour</button>
      <br/>
      <input class="input" placeholder="Input your time" />
      <button class="btn" @click="setMinute">Your time:</button>
      <br/>
      <button class="btn" @click="stopTimer">Stop timer</button>
      <button class="btn" @click="cleanTimer">Clean timer</button>
      <button class="btn" @click="continueTimer">Continue timer</button>
    </div>
    <div class="time">{{ hourTime }}:{{ minuteTime }}:{{ secondTime }}</div>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      hourTime: "00",
      minuteTime: "00",
      secondTime: "00",
      timer: null,
    };
  },
  methods: {
    setMinute(minute, hour) {
      //по идее наоборот
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

        if (
          this.hourTime == 0 &&
          this.minuteTime == 0 &&
          this.secondTime == 0
        ) {
          let result = hour == 0 ? " минут" : " час"; //синтаксические ошибки по обработке данных
          let resultTime = hour == 0 ? minute : hour;

          alert("Прошло " + resultTime + result);
          this.stopTimer();
        }
      }, 1000);
    },

    stopTimer() {
      clearInterval(this.timer);
      clearTimeout(this.timer);
    },
    cleanTimer() {
      this.hourTime = "00";
      this.minuteTime = "00";
      this.secondTime = "00";
    },
    continueTimer() {},
  },
};
</script>

<style>
.btns{
  display: flex;
  
}
.btn {
  margin: 3px;
  font-family: Roboto, sans-serif;
  font-weight: 0;
  font-size: 14px;
  color: #fff;
  background-color: #0066cc;
  padding: 10px 30px;
  border: 2px solid #0066cc;
  box-shadow: rgb(0, 0, 0) 0px 0px 0px 0px;
  border-radius: 1px;
  cursor: pointer;
}
.btn:hover{
  background-color:#0056ac;
}
.input{
  margin: 3px;
  padding: 10px 30px;
  border: 2px solid #0066cc;
}
.time{
  font-family: Roboto, sans-serif;
  font-size: 80px;
  text-align: center;
}
</style>
