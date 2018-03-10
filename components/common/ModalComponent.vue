<template>
  <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Estadisticas de {{user.displayName}} </h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          Times: {{pomodoro.totalPomodoros}} <br>
          Total Times: 00:00:{{pomodoro.time < 10 ? '0' + pomodoro.time : pomodoro.time}}
          <div class="fecha">
            <div 
              v-for="(date, key, index) in pomodoro.date"
              :key="key"
              v-if="index < pageSize"
            >
              {{date}}
            </div>
          </div>
          <button type="button" class="btn" @click="onLoadMore">Cargar más</button>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal" @click="close">Close</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    props: ['pomodoro', 'user'],
    data () {
      return {
        pageSize: 2
      }
    },
    methods: {
      onLoadMore () {
        this.pageSize += 2
      },
      close () {
        this.pageSize = 2
      }
    }
  }
</script>
<style scoped>
  .fecha {
    border: solid grey 1px;
    border-radius: 4px;
    margin: 2px 0;
    padding: 0.5em 0;
  }
</style>
