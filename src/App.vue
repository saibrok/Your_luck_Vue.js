<template>
  <div>
    <button class="btn btn-primary" v-on:click="show = !show">{{ bntText }}</button>
    <transition name="slide">
      <div class="alert" v-bind:class="alert" v-show="show">
        <h2>Your luck: {{ calc() }}</h2>
      </div>
    </transition>
    <Progress v-bind:val="calc() + 2500" v-bind:max="maxNumbers * 500" />
    <hr />
    <div class="timesLeft">{{ timesLeft }} more times left</div>
    <Progress v-bind:val="numbers.length" v-bind:max="maxNumbers"></Progress>
    <button class="btn btn-success" v-on:click="addNumber" v-bind:disabled="done">Add number</button>
    <button class="btn btn-dark" v-bind:disabled="!done" v-on:click="reset">Reset</button>
    <hr />
    <ul class="list-group">
      <li class="list-group-item" v-for="number in numbers" :key="number">{{ number }}</li>
    </ul>
  </div>
</template>

<script>
import Progress from "./components/Progress";

export default {
  components: {
    Progress,
  },
  data() {
    return {
      show: "true",
      numbers: [],
      maxNumbers: 10,
      done: false,
    };
  },
  methods: {
    addNumber() {
      if (this.numbers.length < this.maxNumbers) {
        if (this.numbers.length >= this.maxNumbers - 1) {
          this.done = !this.done;
        }
        return this.numbers.push(Math.floor(Math.random() * 1001 - 500));
      }
    },
    reset() {
      this.numbers.length = 0;
      this.sum = 0;
      this.done = !this.done;
    },
    calc() {
      let sum = 0;
      for (let index = 0; index < this.numbers.length; index++) {
        sum += this.numbers[index];
      }
      return sum;
    },
  },
  computed: {
    bntText() {
      return this.show ? "Hide result" : "Show result";
    },
    timesLeft() {
      return (this.numbers.length - 10) * -1;
    },
    alert() {
      if (this.calc() === 0) {
        return "alert-warning";
      }

      if (this.calc() > 0) {
        return "alert-success";
      }

      if (this.calc() < 0) {
        return "alert-danger";
      }

      return "alert-warning";
    },
  },
};
</script>

<style>
body {
  padding: 1rem;
}

#app {
  margin-top: 1rem;
}

li {
  font-family: "Consolas", "Courier New", monospace;
}

.h2 {
  margin-bottom: 0.5rem;
}

.slide-enter {
  opacity: 0;
}

.slide-enter-active {
  transition: opacity 0.5s;
}

.slide-leave-active {
  transition: opacity 0.5s;
}

.slide-leave-to {
  opacity: 0;
}

.timesLeft {
  margin-bottom: 1rem;
}

.progress {
  margin-bottom: 0.5rem;
}

.btn-primary {
  margin-bottom: 0.5rem;
}

.btn-dark {
  margin-left: 0.5rem;
}
</style>
