<template>
	<f7-page>
	<f7-navbar title="Voucher" link="/" back-link="Back" sliding/>
	<form v-if="codeVoucher==''" id="my-form" class="list-block">
   <ul>
      <li>
         <div class="item-content">
            <div class="item-inner">
               <div class="item-title label">Code Voucher</div>
               <div class="item-input">
                  <input type="text" v-model="voucher" name="name" placeholder="Code Voucher">
               </div>
            </div>
         </div>
      </li>
      <li>
         <div class="item-content">
            <div class="item-inner">
               <div class="item-input">
                 <a href="#" @click="sendvoucher" class="button button-fill button-raised">Send</a>
               </div>
            </div>
         </div>
      </li>
  	</ul>
  	</form>
  	<div v-else>
  	<div class="content-block-title">Your Voucher</div>
    <div class="list-block">
      <ul>
        <li class="item-content">
          <div class="item-media"><i class="icon icon-f7"></i></div>
          <div class="item-inner">
            <div class="item-title">A01</div>
            <!-- <div class="item-after">Label</div> -->
          </div>
        </li>
      </ul>
    </div>
    </div>
	</f7-page>
</template>
<script>
  import axios from 'axios'
  import * as CONFIG from '../config'
  export default {
    data: function () {
      return {
        voucher: null,
        codeVoucher:null
      }
    },
    created:function()
    {
      this.getVoucher
    },
    methods: {
      sendvoucher: function () {
        let url = CONFIG.URL + 'voucher'
        let userid = localStorage.getItem('userid')
        var formData = new FormData()
        formData.append('account', userid)
        formData.append('voucher', this.voucher)
        axios.post(url, formData).then((response) => {
          // console.log(response)
          window.f7.alert('Thank You Your Feedback Has Been Send')
          this.voucher = ''
        })
          .catch(e => {
            window.f7.alert('Sory Try Again Later')
          })
      }
    },
    computed:{
    	getVoucher()
    	{
    	let userid = localStorage.getItem('userid')
      	let url = CONFIG.URL + 'voucher/'+userid;
      	axios.get(url)
        .then(response => {
          let res = response.data
          this.codeVoucher = res.data
          // console.log(this.codeVoucher)
        })
        .catch(e => {
          console.log('error')
        })
    	}
    }
  }
</script>