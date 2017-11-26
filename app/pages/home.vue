<template>
  <f7-page v-if="cekopen==0">
  <f7-navbar :title="$root.config.title" :dynamic-navbar="true" main>
  <f7-nav-right>
    <f7-link icon="icon-bars" open-panel="right"></f7-link>
  </f7-nav-right>
</f7-navbar>
    <!-- <f7-block-title>Welcome</f7-block-title> -->
    <div class="item-inner">
      <img src="../images/promo.jpg" width="100%" style="padding-top:10px;">
    </div>
    <div class="row">
<!--     	<div class="col-50 tablet-25">
        <a href="/menumakanan">
    		<div class="card">
			  <div class="card-content">
			    <div class="card-content-inner menu">
			    	<img src="../images/menures.svg">
			    </div>
			  </div>
			  <div class="card-footer">All Menu</div>
			</div>
      </a>
    	</div> -->
    	<div class="col-50 tablet-25">
        <a href="/category" style="color:black;font-weight: bold">
    		<div class="card">
			  <div class="card-content">
			    <div class="card-content-inner menu">
			    	<img src="../images/menu_64x64.png">
            <br><h4 class="margin-auto">Menu</h4>
			    </div>
			  </div>
			  <!-- <div class="card-footer">Menu Category</div> -->
			</div>
      </a>
    	</div>
    	<div class="col-50 tablet-25">
    		<div class="card">
			  <div class="card-content">
			  	<a href="/paymentdetail" style="color:black;font-weight: bold">
			    <div class="card-content-inner menu">
			    	<img src="../images/billing_64x64.png">
            <br><h4 class="margin-auto">Biling</h4>
			    </div>
			    </a>
			  </div>
			  <!-- <div class="card-footer">Detail Payment</div> -->
			</div>
    	</div>
    	<!-- <div class="col-50 tablet-25">
    		<div class="card">
			  <div class="card-content">
			    <div class="card-content-inner menu">
			    	<img src="../images/chef.svg">
			    </div>
			  </div>
			  <div class="card-footer">Call Waiters</div>
			</div>
    	</div> -->
   <!--  </div>
    <div class="row"> -->
    	<div class="col-50 tablet-25">
        <a href="/favorite" style="color:black;font-weight: bold">
    		<div class="card">
			  <div class="card-content">
			    <div class="card-content-inner menu">
			    	<img src="../images/favorite_64x64.png">
            <br><h4 class="margin-auto">Favorite</h4>
			    </div>
			  </div>
			  <!-- <div class="card-footer">Favorite</div> -->
			</div>
      </a>
    	</div>
    	<div class="col-50 tablet-25">
        <a href="/feedback" style="color:black;font-weight: bold">
    		<div class="card">
			  <div class="card-content">
			    <div class="card-content-inner menu">
			    	<img src="../images/feedback_64x64.png">
            <br><h4 class="margin-auto">Feedback</h4>
			    </div>
			  </div>
			  <!-- <div class="card-footer">Feedback</div> -->
			</div>
      </a>
    	</div>
    	<div class="col-50 tablet-25">
        <a href="/myorder" style="color:black;font-weight: bold">
    		<div class="card">
			  <div class="card-content">
			    <div class="card-content-inner menu">
			    	<img src="../images/order_64x64.png">
            <br><h4 class="margin-auto">My Order</h4>
			    </div>
			  </div>
			  <!-- <div class="card-footer">Proggress</div> -->
			</div>
      </a>
    	</div>
    	<div class="col-50 tablet-25">
        <a href="/voucher" style="color:black;font-weight: bold">
    		<div class="card">
			  <div class="card-content">
			    <div class="card-content-inner menu">
			    	<img src="../images/voucher_64x64.png">
            <br><h4 class="margin-auto">Voucher</h4>
			    </div>
			  </div>
			  <!-- <div class="card-footer">Done</div> -->
			</div>
      </a>
    	</div>
    </div>
  </f7-page>
  <f7-page v-else="cekopen==1">
    <div data-page="login-screen" class="page no-navbar no-toolbar no-swipeback">
    <div class="page-content login-screen-content">
      <div style="padding:10%">
      </div>
            <div class="login-screen-title">Restoran</div>
            <form>
              <div class="list-block">
                <ul>
                  <li class="item-content">
                    <div class="item-inner">
                      <div class="item-title label">Username</div>
                      <div class="item-input">
                        <input type="text" name="username" v-model="username" placeholder="Username">
                      </div>
                    </div>
                  </li>
                  <li class="item-content">
                    <div class="item-inner">
                      <div class="item-title label">Password</div>
                      <div class="item-input">
                        <input type="password" name="password" v-model="password" placeholder="Password">
                      </div>
                    </div>
                  </li>
                </ul>
              </div>
              <div class="list-block">
                <ul>
                  <li class="content-block">
                    <a class="button" @click="login">Sign In</a>
                  </li>
                </ul>
                <div v-if="error" class="list-block-label" style="color:red;font-weight:bold">{{ error }}</div>
              </div>
            </form>
          </div>
        </div>
  </f7-page>
</template>
<style type="text/css">
	.navbar-fixed .navbar, .navbar-through .navbar{
  box-shadow: none;
  }
.popup-overlay.modal-overlay-visible {
    visibility: hidden;
}
	div[class*="col-"] {
  background: #fff;
  text-align: center;
  color: #000;
  /*border: 1px solid #ddd;*/
  border: none;
  padding: 5px;
}
.row {
  margin-bottom: 15px;
}        
a{
  color: black;
}
</style>
<script type="text/javascript">
 // import axios from 'axios'
 import * as CONFIG from '../config'
 // import * as qwest from 'qwest'
var Vue = require('vue')
var VueResource = require('vue-resource')
Vue.use(VueResource)
export default {
   data () {
     return {
       cekopen: 1,
       username: null,
       password: null,
       error: null
     }
   },
   created: function () {
     this.cekopen = localStorage.getItem('cekopen')
   },
   methods: {
     login: function () {
       let url = CONFIG.URL + 'login/'
       this.$http.headers.common.Authorization = 'Basic YXBpOnBhc3N3b3Jk'
       var formData = new FormData()
       formData.append('username', this.username)
       formData.append('password', this.password)
       this.$http.post(url, formData).then((response) => {
         if (response.data.data.length !== 0) {
           localStorage.setItem('cekopen', 0)
           localStorage.setItem('userid', response.data.data[0].id)
           this.cekopen = localStorage.getItem('cekopen')
           this.$router.load({url: '/home/'})
         } else {
           this.error = 'The username or password is incorrect'
           console.log(this.error)
         }
       })
     },
     logout: function () {
       localStorage.setItem('cekopen', 1)
       this.cekopen = localStorage.getItem('cekopen')
       localStorage.removeItem('userid')
       // console.log(this.cekopen)
     },
     redirect: function () {
       return this.$router.load({url: '/home/'})
     }
   }
 }
</script>