<template>
  <div id="app">
    <!-- <login-popup /> -->
    <f7-views>
      <f7-view main url="/home/" navbar-through :dynamic-navbar="$theme.ios" />
    </f7-views>
<div class="panel-overlay"></div>
<div class="panel panel-left panel-cover">
<div class="page-content">
<div class="navbar">
<div class="navbar-inner">
<div class="center">Left Panel</div>
</div>
</div>
    <div class="content-block" style="margin:0px 0px;padding:0px 0px">
    <div class="profile">
     <img src="./images/food-covered-tray-silhouette.svg" width="50%">
     </div>
    </div>
    <div class="list-block">
      <ul>
        <li>
          <a @click="closepanel" href="/menusquare" class="item-link item-content gray">
          <div class="item-media"><i class="f7-icons">menu</i></div>
          <div class="item-inner">
            <div class="item-title">Menu</div>
          </div>
        </a>
        </li>
        <li>
          <a @click="closepanel" href="/categorynew" class="item-link item-content gray">
          <div class="item-media"><i class="f7-icons">data</i></div>
          <div class="item-inner">
            <div class="item-title">Category</div>
          </div>
          </a>
        </li>
        <li>
          <a @click="closepanel" href="/feedback" class="item-link item-content gray">
          <div class="item-media"><i class="f7-icons">email</i></div>
          <div class="item-inner">
           <div class="item-title">Mesage</div>
          </div>
          </a>
        </li>
        <li class="item-content gray">
          <div class="item-media"><i class="f7-icons">phone</i></div>
          <div class="item-inner">
            <div class="item-title">Call Us</div>
          </div>
        </li>
        <li class="item-content gray">
          <div class="item-media"><i class="f7-icons">logout</i></div>
          <div class="item-inner">
            <a @click="logout" href="#" class="item-link"><div class="item-title">Sign Out</div></a>
          </div>
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
}
.margin-auto{
  margin: auto;
}
.card-content-inner.menu{
  padding: 10px !important;
}
</style>
<script>
  export default {
    methods: {
      onF7Init: function () {
        if (global.cordova) {
          document.addEventListener('backbutton', this.$root.$f7Router.framework7.mainView.router.back, false)
        }
      },
      closepanel: function () {
        this.$f7.closePanel()
      },
      logout: function () {
        localStorage.setItem('cekopen', 1)
        console.log('clicked')
        this.$f7.views.main.router.load({url: '/home/'})
      }
    }
  }
</script>