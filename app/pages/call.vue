<template>
	<f7-page>
		<f7-navbar title="Call Waiter" link="/" back-link="Back" sliding/>
		<div class="col-100">
			<img src="../images/waiters.svg" class="col-100 waiter-image">
			<h3 v-if="call" class="call-waiter-loading">{{ text}}</h3>
		</div>
		<a href="#" class="button button-raised button-fill call-waiter-button" @click="callwaiter" :disabled="call"><i class="f7-icons color-white">phone</i> Call</a>
	</f7-page>
</template>
<script type="text/javascript">
  import axios from 'axios'
  import * as CONFIG from '../config'
  export default {
    data: function () {
      return {
        call: false,
        text: 'Calling, please wait ...'
      }
    },
    created: function () {

    },
    methods: {
      callwaiter: function () {
        this.call = true
        let userid = localStorage.getItem('userid')
        let url = CONFIG.URL + 'call/' + userid
        axios.get(url)
          .then(response => {
            // let res = response.data.data
            this.text = 'Saya segera kesana'
          })
          .catch(e => {
            console.log('error')
            this.$f7.alert('Network Error')
          })
        setTimeout(() => {
          this.call = false
          this.text = 'Calling, please wait ...'
        }, 10000)
      }
    }
  }
</script>
<style type="text/css">
	img.waiter-image {
    margin-left: 20%;
    margin-right: 20%;
    margin-top: 5%;
    margin-bottom: 5%;
    width: 150vw;
    width: inherit;
}
.call-waiter-loading{
	text-align: center;
	font-family: Roboto, Noto, Helvetica, Arial, sans-serif;
	color: #6e6e6e;
}
.call-waiter-button{
	margin-left: 5%;
	margin-right: 5%;
	background: #CC0D52 !important;
}
</style>