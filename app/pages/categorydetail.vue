<template>
  <f7-page>
  	<f7-navbar :title="title" link="/" back-link="Back" sliding/>

   <!--  <f7-searchbar
    cancel-link="Cancel"
    search-list="#search-list"
    placeholder="Cari Menu"
    :clear-button="true"
    @searchbar:search="onSearch"
    @searchbar:enable="onEnable"
    @searchbar:disable="onDisable"
    @searchbar:clear="onClear">
  </f7-searchbar>
  <f7-list class="searchbar-not-found">
    <f7-list-item title="Pencarian Tidak Ditemukan"></f7-list-item>
  </f7-list> -->
<f7-list class="searchbar-found" id="search-list">
    <div class="list-block media-list" v-for="item in data">
    <ul>
        <li>
            <div class="item-content">
                <div class="item-media">
                    <img v-if="!item.image" src="../images/no-image.svg" width="90">
                    <img v-if="item.image" :src="item.image" width="90">
                </div>
                <div class="item-inner">
                    <div class="item-title-row">
                        <div class="item-title">{{ item.name }}</div>
                    </div>
                    <div class="item-text">{{ item.time }} Minutes</div>
                    <div class="item-text">{{ formatPrice(item.price) }}</div>
                    <a :href="linked(item)"><label class="badge bg-green buy-item">Detail</label></a>
                </div>
            </div>
        </li>
    </ul>
</div>  
</f7-list>
  </f7-page>
</template>

<style type="text/css">
.navbar-fixed .navbar, .navbar-through .navbar{
  box-shadow: none;
}
	.buy-item{
		position: absolute;
		top:50px;
		right: 15px;
		
		bottom: 30px;
	}
	label.badge.bg-green.buy-item {
    width: 60px;
    text-align: center;
    margin: 5px;
    font-size: 15px;
    height: 25px;
}
.list-block.media-list{
	margin: 5px;
}

</style>
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
        return '/detail/' + item.id + '/' + item.name
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