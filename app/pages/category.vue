<template>
	<f7-page>
		<f7-navbar title="Category" link="/" back-link="Back" sliding/>
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
    <div class="list-block">
      <ul>
      	<div v-for="category in datas">
      	<a :href="linked(category)" class="item-link">
        <li class="item-content">
          <div class="item-media"><i class="f7-icons">tags_fill</i></div>
          <div class="item-inner">
            <div class="item-title">{{ category.name }}</div>
            <div class="item-after"></div>
          </div>
        </li>
    	</a>
    	</div>
      </ul>
      <!-- <div class="list-block-label">List block label text goes here</div> -->
    </div>
    </f7-list>

	</f7-page>
</template>
<script>
  import axios from 'axios'
  import * as CONFIG from '../config'
export default {
    data: function () {
      return {
        datas: [],
        ready: false,
        items: (function () {
          var it = []
          for (var i = 0; i < 100; i++) it.push(i + 1)
          return it
        })()
      }
    },
    created: function () {
      let myApp = this.$f7
      myApp.showIndicator()
      let url = CONFIG.URL + 'menu'
      axios.get(url)
        .then(response => {
          let res = response.data
          this.datas = res.data
          this.ready = true
          if (this.ready) {
            myApp.hideIndicator()
          }
        })
        .catch(e => {
          console.log('error')
        })
    },
    methods: {
      linked: function (item) {
        // window.f7.alert(item.id);
        return '/categorydetail/' + item.id + '/' + item.name
      },
      alertclickfalse: function () {
        return this.datas.id
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