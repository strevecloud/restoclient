<template>
<f7-page>
<f7-navbar title="Inprogress" link="/" back-link="Back" sliding/>
<div class="content-block-title">Inprogress</div>
<div class="list-block">
  <ul>
  	<div v-for="item in data">
    <Countdown :name="item.name" status="status" :deadline="item.ended"></Countdown>
    </div>
  </ul>
</div>
</f7-page>
</template>
<script>
  import Countdown from 'vuejs-countdown'
  import axios from 'axios'
  import * as CONFIG from '../config'
  export default {
    components: {
      Countdown
    },
    data () {
      return {
        data: []
      }
    },
    created: function () {
      let userid = localStorage.getItem('userid')
      let url = CONFIG.URL + 'order/' + userid
      let myApp = this.$f7
      myApp.showIndicator()
      axios.get(url)
        .then(response => {
          let res = response.data.data
          this.data = res
          console.log(res)
          this.ready = true
          if (this.ready) {
            myApp.hideIndicator()
          }
        })
        .catch(e => {
          console.log('error')
          myApp.hideIndicator()
          this.$f7.alert('Network Error')
        })
    }
  }
</script>