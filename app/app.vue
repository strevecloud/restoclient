<template>
  <div id="app">
    <login-popup />
    <f7-views>
      <f7-view main url="/home/" navbar-through :dynamic-navbar="$theme.ios" />
    </f7-views>
<div class="panel-overlay"></div>
<div class="panel panel-left panel-cover">
<div class="page-content">
<div class="navbar">
<div class="navbar-inner">
<div class="center">{{ nameresto }}</div>
</div>
</div>
    <div class="content-block" style="margin:0px 0px;padding:0px 0px">
    <div class="profile">
     <img :src="logo" width="50%">
     </div>
    </div>
    <div class="list-block">
      <ul>
        <li>
          <a @click="closepanel" href="/categorynew" class="item-content gray">
          <div class="item-media"><i class="f7-icons">data</i></div>
          <div class="item-inner">
            <div class="item-title">Category</div>
          </div>
          </a>
        </li>
        <li>
          <a @click="closepanel" href="/favorite" class="item-content gray">
          <div class="item-media"><i class="f7-icons">star</i></div>
          <div class="item-inner">
           <div class="item-title">Favorite</div>
          </div>
          </a>
        </li>
        <li>
          <a @click="closepanel" href="/myorder" class="item-content gray">
          <div class="item-media"><i class="f7-icons">compose</i></div>
          <div class="item-inner">
           <div class="item-title">My Order</div>
          </div>
          </a>
        </li>
        <li>
          <a @click="closepanel" href="/voucher" class="item-content gray">
          <div class="item-media"><i class="f7-icons">ticket</i></div>
          <div class="item-inner">
            <div class="item-title">Voucher</div>
          </div>
        </a>
        </li>
        <li>
          <a @click="closepanel" href="/paymentdetail" class="item-content gray">
          <div class="item-media"><i class="f7-icons">card</i></div>
          <div class="item-inner">
            <div class="item-title">Biling</div>
          </div>
        </a>
        </li>
        <li>
          <a @click="closepanel" href="/feedback" class="item-content gray">
          <div class="item-media"><i class="f7-icons">email</i></div>
          <div class="item-inner">
           <div class="item-title">Feedback</div>
          </div>
          </a>
        </li>
        <li>
          <a @click="closepanel" href="/call" class="item-content gray">
          <div class="item-media"><i class="f7-icons">phone</i></div>
          <div class="item-inner">
            <div class="item-title">Call Us</div>
          </div>
        </a>
        </li>
      </ul>
    </div>
  </div>
</div>
  </div>
</template>
<style type="text/css">
div[class*="col-"]{
  background-color: #F5F5F5 !important
}
	.navbar-fixed .navbar, .navbar-through .navbar{
  box-shadow: none;
}
.profile{
  text-align: center;
  padding: 10px;
}
.no-margin{
  margin: 0px;
}
.navbar-inner{
  background-color: #CC0D52;
}
.navbar{
   box-shadow: none !important;
}
.page{
  background-color: #F5F5F5 !important;
}
.searchbar{
  background-color: #CC0D52 !important;
}
.item-content{
  background-color: white;
  margin-bottom: 10px;
}
.list-block{
  margin: 10px 0 !important;
}
.list-block .item-link, .list-block .list-button{
  overflow: inherit !important;
}
.panel{
   background-color: #F5F5F5 !important;
}
li.item-content.gray {
    background-color: #F5F5F5;
}
.theme-blue .button.button-fill {
  background: #CC0D52 !important;
}
a.button.button-fill.button-raised.pink{
   background: #CC0D52 !important;
}
.item-content.gray{
   background-color: #F5F5F5;
   color: black;
}
.margin-auto{
  margin: auto;
}
.card-content-inner.menu{
  padding: 10px !important;
}
.item-inner.home{
   background-color: #F5F5F5; 
}
</style>
<script>
  import axios from 'axios'
  import * as CONFIG from './config'
  export default {
    data: function () {
      return {
        data: [],
        logo: '',
        nameresto: ''
      }
    },
    created: function () {
      let url = CONFIG.URL + 'setting'
      axios.get(url)
        .then(response => {
          let res = response.data.data
          this.data = res
          this.logo = res[0].logo
          this.nameresto = res[0].name
          // console.log(res[0])
        })
        .catch(e => {
          console.log(e)
          this.$f7.alert('Network Error')
        })
    },
    methods: {
      onF7Init: function () {
        if (global.cordova) {
          document.addEventListener('backbutton',
            this.$root.$f7Router.framework7.mainView.router.back,
            alert(this.$root.$f7Router.framework7.mainView.route.url), false)
        }
      },
      closepanel: function () {
        this.$f7.closePanel()
      },
      logout: function () {
        localStorage.setItem('cekopen', 1)
        console.log('clicked')
        this.$f7.views.main.router.load({
          url: '/home/'
        })
      }
    }
  }
</script>