<template>
  <div>
    <header-component></header-component>
    <div class="container min-full-height">
      <div class="main-content row">
        <div class="col-sm-12">
          <h2 class="title">Your statistics - {{user.displayName}}</h2>
          <p>Total Pomodoros: {{totalPomodoros}}</p>
        </div>
      </div>
    </div>
    <footer-component></footer-component>
  </div>
</template>
<script>
  import { HeaderComponent, FooterComponent } from '~/components/common'
  import {mapGetters, mapActions} from 'vuex'
  export default {
    middleware: 'authenticated',
    computed: {
      ...mapGetters({
        totalPomodoros: 'getTotalPomodoros',
        user: 'getUser'
      })
    },
    components: {
      HeaderComponent,
      FooterComponent
    },
    methods: {
      ...mapActions(['readWorkoutStats'])
    },
    mounted () {
      this.readWorkoutStats()
    }
  }
</script>
