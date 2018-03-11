<template>
  <div>
    <header-component></header-component>
    <modal-component :details="dates"></modal-component>
    <div class="container min-full-height">
      <div class="main-content row">
        <div class="col-sm-12">
          <h2 class="title">Your statistics - {{user.displayName}} </h2>
          <p>Total Pomodoros: {{totalPomodoros}}</p>
        </div>
        <div class="content">
          <div 
            class="progress"
            v-for="(date, key, index) in workouts"
            :key="key"
            :style="{background: index % 2 === 0 ? 'lightgrey' : 'darkgrey'}"
            :getWidth="getWidth(date.count)"
            @click="upDate(date)"
            data-toggle="modal" 
            data-target="#exampleModal"
          >
            <div 
              class="progress-bar"
              :style="{width: date.count * 100 / max + '%', backgroundColor: colors[index % colors.length]}"
              role="progressbar" 
            >
              <span class="left"> {{ date.name }} </span>
              <span class="right"> {{ date.count }} </span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <footer-component></footer-component>
  </div>
</template>
<script>
  import { HeaderComponent, FooterComponent } from '~/components/common'
  import { ModalComponent } from '~/components/workouts'
  import {mapGetters, mapActions} from 'vuex'
  export default {
    data () {
      return {
        colors: ['red', 'blue', 'green', 'brown'],
        max: 0,
        dates: ''
      }
    },
    middleware: 'authenticated',
    computed: {
      ...mapGetters({
        totalPomodoros: 'getTotalPomodoros',
        workouts: 'getWorkoutStats',
        user: 'getUser'
      })
    },
    components: {
      HeaderComponent,
      FooterComponent,
      ModalComponent
    },
    methods: {
      ...mapActions(['readWorkoutStats']),
      getWidth (n) {
        if (n >= this.max) {
          this.max = n
        }
      },
      upDate (d) {
        this.dates = d
      }
    },
    mounted () {
      this.readWorkoutStats()
    }
  }
</script>
<style scoped>
  .content {
    background-color: rgb(236, 233, 233);
    width: 90%;
    padding-bottom: 1.5em;
    margin: auto;
  }
  .progress {
    margin-top: 2em!important;
    padding: 1em 0;
    width: 90%;
  }
  .left {
    float: left;
    margin-left: 1em;
  }
  .right {
    float: right;
    margin-right: 1em;
  }
</style>
