<template>
	<f7-page>
		<f7-navbar title="Feedback" link="/" back-link="Back" sliding/>
<form id="my-form" class="list-block">
   <ul>
      <li>
         <div class="item-content">
            <div class="item-inner">
               <div class="item-title label">Nama</div>
               <div class="item-input">
                  <input type="text" v-model="feedback_name" name="name" placeholder="Nama Lengkap">
               </div>
            </div>
         </div>
      </li>
     <!--  <li>
         <div class="item-content">
            <div class="item-inner">
               <div class="item-title label">E-mail</div>
               <div class="item-input">
                  <input type="email" v-model="email" name="email" placeholder="E-mail">
               </div>
            </div>
         </div>
      </li> -->
      <li>
         <div class="item-content">
            <div class="item-inner">
               <div class="item-title label">Komentar</div>
               <div class="item-input">
                  <textarea name="feedback" v-model="feedback_description" placeholder="Komentar"></textarea>
               </div>
            </div>
         </div>
      </li>
      <li>
         <div class="item-content gray">
            <div class="item-inner">
               <div class="item-input">
                 <a href="#" @click="sendfeedback" class="button button-fill button-raised pink">Send</a>
               </div>
            </div>
         </div>
      </li>
   </ul>
</form>
	</f7-page>
</template>
<script>
  import axios from 'axios'
  import * as CONFIG from '../config'
  export default {
    data: function () {
      return {
        feedback_name: null,
        feedback_description: null
      }
    },
    methods: {
      sendfeedback: function () {
        let url = CONFIG.URL + 'feedback'
        let userid = localStorage.getItem('userid')
        var formData = new FormData()
        formData.append('account', userid)
        formData.append('feedback_name', this.feedback_name)
        formData.append('feedback_description', this.feedback_description)
        axios.post(url, formData).then((response) => {
          // console.log(response)
          window.f7.alert('Thank You Your Feedback Has Been Send')
          this.feedback_name = ''
          this.feedback_description = ''
        })
          .catch(e => {
            window.f7.alert('Sory Try Again Later')
          })
      }
    }
  }
</script>