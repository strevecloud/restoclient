<template>
  <f7-page>
  	<f7-navbar title="Menu Makanan" link="/" back-link="Back" sliding/>

    <f7-searchbar
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
  </f7-list>
<f7-list class="searchbar-found" id="search-list">
    <div class="list-block media-list" v-for="item in data" :key="item.id">
    <ul>
        <li>
            <div class="item-content">
                <div class="item-media">
                    <img :src="item.image" width="70">
                </div>
                <div class="item-inner" :title="'Item ' + item">
                    <div class="item-title-row">
                        <div class="item-title">{{ item.name }}</div>
                    </div>
                    <div class="item-subtitle"><br/></div>
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
	margin: 10px;
}
</style>
<script>
  import * as CONFIG from '../config'
  import axios from 'axios'
  export default {
    data: function () {
      return {
        data: [],
        items: (function () {
          var it = []
          for (var i = 0; i < 100; i++) it.push(i + 1)
          return it
        })()
      }
    },
    created: function () {
      let url = CONFIG.URL + 'menu'
      axios.get(url)
        .then(response => {
          // JSON responses are automatically parsed.
          let res = response.data
          this.data = res
          // console.log(res)
        })
        .catch(e => {
          console.log('error')
        })
    },
    methods: {
      linked: function (item) {
        // window.f7.alert(item.id);
        return '/detail/' + item.id + '/' + item.name
      },
      backto: function () {
        this.$f7.views.main.router.back()
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