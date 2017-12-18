<template>
	<f7-page>
		<f7-navbar title="Category" link="/" back-link="Back" sliding/>
		 <div class="content-block rectangle">
		    <div class="row menu-category" v-for="category in datas">
		      <div class="col-100 image-category">
		      <a :href="linked(category)" class="item-link">
		      	<div class="card demo-card-header-pic rectangle">
				  <div :style="{ 'background-image': 'url(' + category.background + ')' }" valign="bottom" class="card-header color-white no-border rectangle">
				  	<span class="center-title">{{ category.name }}</span>
				  </div>
				</div>
				</a>
		      </div>
		      <!-- <div class="col-100 image-category">
		      	<div class="card demo-card-header-pic rectangle">
				  <div style="background-image:url('https://skounis.s3.amazonaws.com/mobile-apps/restaurant-ionic/_demonstration/assets/cat-a-5-1.png')" valign="bottom" class="card-header color-white no-border rectangle">
				  	<span class="center-title">Cheesy Rosemary Rolls</span>
				  </div>
				</div>
		      </div> -->
		      <!-- <div class="col-100 image-category">
		      	<div class="card demo-card-header-pic rectangle">
				  <div style="background-image:url('https://skounis.s3.amazonaws.com/mobile-apps/restaurant-ionic/_demonstration/assets/cat-b-4-1.png')" valign="bottom" class="card-header color-white no-border rectangle">
				  	<span class="center-title">Feta Cheese Dip</span>
				  </div>
				</div>
		      </div> -->
		      <!-- <div class="col-100 image-category">
		      	<div class="card demo-card-header-pic rectangle">
				  <div style="background-image:url('https://skounis.s3.amazonaws.com/mobile-apps/restaurant-ionic/_demonstration/assets/cat-b-5-1.png')" valign="bottom" class="card-header color-white no-border rectangle">
				  	<span class="center-title">Feta Cheese Dip</span>
				  </div>
				</div>
		      </div> -->
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
        return '/menusquare/' + item.id + '/' + item.name
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
<style type="text/css">
 .col-100.image-category {
  text-align: center;
  border: hidden;
  padding: 0 0 0 0;
}
.card-header.color-white.no-border.rectangle {
    height: 40vw;
    box-sizing: unset !important;
    box-shadow: inset 0 0 0 1000px rgba(0,0,0,.3);
}
.row.menu-category {
  margin-bottom: 0px !important;
}          
.content-block.rectangle {
    padding: 0px !important;
    margin: 0px !important;
    margin-top: 0px !important;
    /*opacity: 0.5;*/
}
.content-block.rectangle:before {
  background-color: black;
  position: absolute;
  left: 0; right: 0;
  top: 0; bottom: 0;
  background: rgba(0,0,0,0.6);
}
.center-title{
	margin: auto;
	/*box-shadow: inset 0 0 0 1000px rgba(0,0,0,.5);*/
}
</style>