<template>
  <f7-page v-if="cekopen==0">
    <f7-navbar :title="navname" :dynamic-navbar="true" main>
      <f7-nav-right>
        <f7-link icon="icon-bars" open-panel="right"></f7-link>
      </f7-nav-right>
    </f7-navbar>
    <div class="content-block home">
    <swiper :options="swiperOption">
        <swiper-slide v-for="photo in banners" :style="{ 'background-image': 'url(' + photo.banner + ')' }" width="100vw">
          <div class="item-subtitle">
            <h3 class="judul-slide">{{ photo.title }}</h3>
          </div>
        </swiper-slide>
        <div class="swiper-pagination" slot="pagination"></div>
      </swiper>
    </div>
    <div class="list-block">
      <ul>
        <li class="item-content">
          <div class="item-inner">
              <a href="#tab1" class="tab-link active">
              <div class="chip">
                <div class="chip-label">Favorite</div>
              </div>
              </a>
              <a href="/categorynew">
              <div class="chip">
                <div class="chip-label">Category</div>
              </div>
              </a>
          </div>
        </li>
      </ul>
    </div>
     <div class="tabs">
    <!-- Tab 1 -->
    <div id="tab1" class="tab active">
      <div class="content-block-title title-tab">Favorite</div>
      <div class="content-block menu">
        <div class="row">
          <div class="col-50 tablet-33 padding-square" v-for="item in data.slice(0, 4)">
            <a :href="linked(item)">
            <div class="card demo-card-header-pic">
          <!-- <div style="background-image:url('https://skounis.s3.amazonaws.com/mobile-apps/restaurant-ionic/_demonstration/assets/cat-a-1-1.png')" valign="bottom" class="square"></div> -->
          <div :style="{ 'background-image': 'url(' + item.photo + ')' }" valign="bottom" class="square"></div>
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
<script>
  import Vue from 'vue'
  import axios from 'axios'
  import * as CONFIG from '../config'
  import VueAwesomeSwiper from 'vue-awesome-swiper'
  var VueResource = require('vue-resource')
  Vue.use(VueResource)
  Vue.use(VueAwesomeSwiper)
  export default {
    data () {
      return {
        swiperOption: {
          pagination: '.swiper-pagination',
          paginationClickable: true,
          spaceBetween: 30,
          loop: true,
          centeredSlides: true,
          autoplay: 10000,
          autoplayDisableOnInteraction: false
        },
        data: [],
        title: '',
        ready: false,
        cekopen: 1,
        username: null,
        password: null,
        error: null,
        banners: [],
        navname: ''
      }
    },
    created: function () {
      this.getname()
      this.cekopen = localStorage.getItem('cekopen')
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
          this.$f7.alert('Network Error2')
        })

      let urlbanner = CONFIG.URL + 'banner/'
      axios.get(urlbanner)
        .then(response => {
          this.banners = response.data.data
          // console.log(this.banners)
        })
        .catch(e => {
          console.log('error')
          myApp.hideIndicator()
          this.$f7.alert('Network Error')
        })
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
            this.$router.load({
              url: '/home/'
            })
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
      },
      redirect: function () {
        return this.$router.load({
          url: '/home/'
        })
      },
      linked: function (item) {
        return '/detailmenu/' + item.id + '/' + item.name
      },
      alertclickfalse: function () {
        return this.data.id
      },
      formatPrice (value) {
        let val = (value / 1).toFixed(2).replace('.', ',')
        return 'Rp ' + val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
      },
      getname: function () {
        let url = CONFIG.URL + 'setting'
        axios.get(url)
          .then(response => {
            let res = response.data.data
            this.navname = res[0].name
            console.log(res[0])
          })
          .catch(e => {
            console.log('error')
            this.$f7.alert('Network Error2')
          })
      }
    }
  }
</script>
<style>
.swiper-slide {
  background: #fff;
  box-sizing: border-box;
  border: 1px solid #ccc;
  background-position: 50% 50%;
  background-size: cover;
}
.swiper-slide span {
  text-align:center;
  display:block;
  margin: 20px;
  font-size:21px;
}
.swiper-container {
  margin: 35px 0;
  width: 100%;
  height: 60vw !important;
}
img.carouser-image {
 width: 100vw;
  height: auto;
  overflow: hidden;
}
.content-block.home{
  margin: 0px;
  padding: 0px;
  box-sizing: unset;
}
.swiper-container{
  margin: 0px;
  height: 40vw;
}
.swiper-slide{
  background-color: #F5F5F5 !important;
  border: unset !important;
}
.item-subtitle {
    background: rgba(255,255,255,.8);
    position: absolute;
    left: 0;
    right: 0;
    bottom: 6px;
    margin: 0;
    border: 0;
    padding-bottom: 40px;
}
.judul-slide{
  margin: 0 0 -10px;
  font-weight: 400;
  font-size: 16px;
  font-family: Roboto,"Segoe UI",sans-serif;
  color: #6e6e6e;
  padding: 7px 5px 2px 14px;
}
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
  font-size: 14px !important;
  color: #6e6e6e;
  font-weight: 500;
  font-family: "-apple-system","Helvetica Neue",Roboto,"Segoe UI",sans-serif;
  margin: auto;
  text-align: center;
  }
 .col-50.padding-square {
    padding: 0px !important;
    padding-bottom: 15px !important;
}
.content-block-title.title-tab {
  padding-top: unset !important;
  text-align: center;
  font-size: 18px !important;
}
</style>