<template>
  <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel"> {{ details.name }} </h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close" @click="close()">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          Times: {{ details.count }} <br>
          Total Time: {{formatTime(details.time)}}
        </div>
        <div>
          <ul>
            <li 
              v-for="(date, index) in details.date"
              :key="date.key"
              v-if="index < pageSize"
            >
              {{ date }}
            </li>
          </ul>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-sm" @click="onLoadMore">Cargar más</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    props: ['details'],
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
      },
      formatTime (time) {
        let hours = Math.floor(time / 3600)
        let minutes = Math.floor((time - (hours * 3600)) / 60)
        let seconds = time - (hours * 3600) - (minutes * 60)
        if (hours < 10) hours = '0' + hours
        if (minutes < 10) minutes = '0' + minutes
        if (seconds < 10) seconds = '0' + seconds
        return hours + ':' + minutes + ':' + seconds
      }
    }
  }
</script>
<style scoped>
  .btn {
    width: 100%;
  }
</style>

