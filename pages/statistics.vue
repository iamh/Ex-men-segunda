<template>
  <div>
    <header-component></header-component>
    <modal-component :pomodoro="pomo" :user="user"></modal-component>
    <div class="container min-full-height">
      <h2 class="title">Statistics</h2>
      <div class="main-content row">
        <div class="col-sm-12">
          <p>Total Pomodoros: {{totalPomodoros}}</p>
          <div
            class="progress"
            v-for="(pomodoro, key, index) in pomodoroStatics"
            :key="key"
            :getWidth="getWidth(pomodoro.totalPomodoros)"
            :class="index % 2 === 0 || index === 0 ? 'grey' : 'more-grey'"
            @click="test(pomodoro)"
            data-toggle="modal"
            data-target="#exampleModal"
          >
            <div 
              class="progress-bar"
              :class="index % 4 === 0 || index === 0 ? 'rojo' : index % 4 === 1 || index === 1 ? 'azul' : index % 5 === 1 || index === 2 ? 'verde' : 'marron'"
              role="progressbar"
              :style="pomodoro.totalPomodoros === mayor ? 'width: 100%' : 'width:' + pomodoro.totalPomodoros / mayor * 100 + '%'"
              aria-valuenow="60" 
              aria-valuemin="0" 
              aria-valuemax="100"
            >
              <span class="left"> {{pomodoro.name}} </span>
              <span class="right"> {{pomodoro.totalPomodoros}} </span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <footer-component></footer-component>
  </div>
</template>
<script>
  import { HeaderComponent, FooterComponent, ModalComponent } from '~/components/common'
  import {mapGetters, mapActions} from 'vuex'
  export default {
    data () {
      return {
        mayor: 0,
        modal: false,
        pomo: ''
      }
    },
    middleware: 'authenticated',
    computed: {
      ...mapGetters({
        totalPomodoros: 'getTotalPomodoros',
        pomodoroStatics: 'getPomodoroStatics',
        user: 'getUser'
      })
    },
    methods: {
      ...mapActions(['readWorkoutsStatics']),
      getWidth (n) {
        if (n >= this.mayor) {
          this.mayor = n
        }
      },
      test (p) {
        this.modal = true
        this.pomo = p
      }
    },
    components: {
      HeaderComponent,
      FooterComponent,
      ModalComponent
    },
    mounted () {
      this.readWorkoutsStatics(this.user.uid)
    }
  }
</script>
<style scoped>
  .main-content {
    background-color: lightgray;
  }
  .container {
    margin-bottom: 5em;
  }
  .more-grey{
    background-color: rgb(138, 132, 132);
  }
  .progress {
    margin-top: 2em!important;
    padding: 1em 0;
  }
  .rojo{
    background-color: red;
  }
  .azul {
    background-color: blue;
  }
  .verde {
    background-color: green;
  }
  .marron {
    background-color: brown;
  }
  .left{
    float: left;
    margin-left: 1em;
  }
  .right {
    float: right;
    margin-right: 1em;
  }
</style>
