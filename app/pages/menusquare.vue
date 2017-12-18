<template>
	<f7-page>
		<f7-navbar :title="title" link="/" back-link="Back" sliding/>
<!-- 		<f7-toolbar tabbar bottom>
		<div class="toolbar-inner">
		<a href="#tab1" class="tab-link">
            <i class="f7-icons">home</i>
            <span class="tabbar-label">Home</span>
        </a>
        <a href="/listmenu" class="toolbar-link">
            <i class="f7-icons">menu</i>
            <span class="toolbar-label">List</span>
        </a>
        <a href="#tab2" class="tab-link">
             <i class="f7-icons">star</i>
            <span class="tabbar-label">Favorite</span>
        </a>
        <a href="/categorynew" class="toolbar-link">
            <i class="f7-icons">book</i>
            <span class="toolbar-label">Menu</span>
        </a>
    </div>
		</f7-toolbar> -->
	  <div class="content-block menu">
	      <div class="row">
	        <div class="col-50 tablet-33 padding-square" v-for="item in data">
	        	<div class="card demo-card-header-pic">
          <a :href="linked(item)">
          <div :style="{ 'background-image': 'url(' + item.photo + ')' }" valign="bottom" class="square"></div>
				  <div class="card-content">
				    <div class="card-content-inner text">
				    	<h3 class="single-title-menu">{{ item.name }}</h3>
				    	<h4 class="single-title-menu">{{ formatPrice(item.price) }}</h4>
				    </div>
				  </div>
        </a>
				</div>
	        </div>
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
        data: [],
        title: '',
        ready: false,
        items: (function () {
          var it = []
          for (var i = 0; i < 100; i++) it.push(i + 1)
          return it
        })()
      }
    },
    created: function () {
      let routeparam = this.$route.params.id
      this.title = this.$route.params.name
      let url = CONFIG.URL + 'menu/'
      let urldetail = url + routeparam
      let myApp = this.$f7
      myApp.showIndicator()
      axios.get(urldetail)
        .then(response => {
          // JSON responses are automatically parsed.
          let res = response.data
          this.data = res.data
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
    },
    methods: {
      linked: function (item) {
        // window.f7.alert(item.id);
        return '/detailmenu/' + item.id + '/' + item.name
      },
      alertclickfalse: function () {
        return this.data.id
      },
      formatPrice (value) {
        let val = (value / 1).toFixed(2).replace('.', ',')
        return 'Rp ' + val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
      },
      onSearch: function (query, found) {
        console.log('search', query)
        console.log(found)
      },
      onClear: function (event) {
        console.log('clear')
      },
      onEnable: function (event) {
        console.log('enable')
      },
      onDisable: function (event) {
        console.log('disable')
      }
    }
  }
</script>
<style type="text/css">
.content-block.menu{
	margin: 5px;
	padding: 0px !important;
}
.card{
	margin: 0px !important;
}
.square {
    width: 100%;
    padding-bottom: 100%;
    background-size: cover;
    background-position: center;
}
.menu-pic{
  width: 100%;
  height: 100%;
  position: relative;
  background-size: cover;
  overflow: hidden;
}
.card-content-inner.text {
	padding: 0px !important;
    padding-bottom: 16px !important;
}
.single-title-menu{
 	font-size: 14px;
 	color: #6e6e6e;
 	font-weight: 500;
 	font-family: "-apple-system","Helvetica Neue",Roboto,"Segoe UI",sans-serif;
 	margin: auto;
  }
 .col-50.padding-square {
    padding: 0px !important;
    padding-bottom: 15px !important;
}
</style>