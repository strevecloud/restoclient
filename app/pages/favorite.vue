<template>
  <f7-page>
  	<f7-navbar title="Favorite" link="/" back-link="Back" sliding/>
      <div class="content-block menu">
        <div class="row">
          <div class="col-50 tablet-33 padding-square" v-for="item in data">
            <a :href="linked(item)">
            <div class="card demo-card-header-pic">
          <div style="background-image:url('https://skounis.s3.amazonaws.com/mobile-apps/restaurant-ionic/_demonstration/assets/cat-a-1-1.png')" valign="bottom" class="square"></div>
          <div class="card-content">
            <div class="card-content-inner text">
              <h3 class="single-title-menu">{{ item.name }}</h3>
              <h4 class="single-title-menu">{{ formatPrice(item.price) }}</h4>
            </div>
          </div>
        </div>
        </a>
          </div>
        </div>
    </div>
  </f7-page>
</template>

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
<script>
  import axios from 'axios'
  import * as CONFIG from '../config'
export default {
    data: function () {
      return {
        data: [],
        title: '',
        ready: false
      }
    },
    created: function () {
      let url = CONFIG.URL + 'favorite'
      let myApp = this.$f7
      myApp.showIndicator()
      axios.get(url)
        .then(response => {
          let res = response.data.data
          this.data = res
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
        return '/detailmenu/' + item.id + '/' + item.name
      },
      alertclickfalse: function () {
        return this.data.id
      },
      formatPrice (value) {
        let val = (value / 1).toFixed(2).replace('.', ',')
        return 'Rp ' + val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
      }
    }
  }
</script>