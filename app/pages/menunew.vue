<template>
	<f7-page v-if="cekopen==0">
		<f7-navbar :title="$root.config.title" :dynamic-navbar="true" main>
      <f7-nav-right>
        <f7-link icon="icon-bars" open-panel="right"></f7-link>
      </f7-nav-right>
    </f7-navbar>
    <div class="content-block home">
    <swiper :options="swiperOption">
        <swiper-slide v-for="n in 10" style="background-image:url('https://recipeland.com/images/r/17725/ea4a1cd2d6d882ba37d2_1024.jpg');width:100vw;">
        	<!-- <img class="carouser-image" src="https://skounis.s3.amazonaws.com/mobile-apps/restaurant-ionic/_demonstration/assets/cat-d-5-1.png"> -->
          <div class="item-subtitle">
            <h3 class="judul-slide">Salmon Fillet</h3>
          </div>
        </swiper-slide>
        <div class="swiper-pagination" slot="pagination"></div>
      </swiper>
    </div>
    <div class="list-block">
      <ul>
        <li class="item-content">
          <div class="item-inner">
              <a href="#tab1" class="tab-link">
              <div class="chip">
                <div class="chip-label">Recomended</div>
              </div>
              </a>
              <a href="#tab2" class="tab-link">
              <div class="chip">
                <div class="chip-label">Favorite</div>
              </div>
              </a>
             <!--  <a href="#tab3" class="tab-link">
              <div class="chip">
                <div class="chip-label">Popular</div>
              </div>
              </a> -->
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
    <!-- Tab 1, active by default -->
    <div id="tab1" class="tab active">
      <div class="content-block-title title-tab">Recomended</div>
      <div class="content-block menu">
        <div class="row">
          <div class="col-50 tablet-33 padding-square" v-for="n in 6">
            <a href="/detailmenu">
            <div class="card demo-card-header-pic">
          <div style="background-image:url('http://rasasayange.co.id/assets/images/large_resep_85_mie%20ayam%202.jpg')" valign="bottom" class="square"></div>
          <div class="card-content">
            <div class="card-content-inner text">
              <h3 class="single-title-menu">Mie Ayam</h3>
              <h4 class="single-title-menu">Rp 14.000</h4>
            </div>
          </div>
        </div>
        </a>
          </div>
        </div>
    </div>
    </div>
    <!-- Tab 2 -->
    <div id="tab2" class="tab">
      <div class="content-block-title title-tab">Favorite</div>
      <div class="content-block menu">
        <div class="row">
          <div class="col-50 tablet-33 padding-square" v-for="item in data.slice(0, 4)">
            <a href="/detailmenu">
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
    </div>
    <!-- Tab 3 -->
    <!-- <div id="tab3" class="tab">
      <div class="content-block">
        <p>This is tab 3 content</p>
      </div>
    </div> -->
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
          // autoplay: 2500,
          autoplayDisableOnInteraction: false
        },
        data: [],
        title: '',
        ready: false,
        cekopen: 1,
        username: null,
        password: null,
        error: null
      }
    },
    created: function () {
      // let routeparam = this.$route.params.id
      // this.title = this.$route.params.name
      this.cekopen = localStorage.getItem('cekopen')
      let url = CONFIG.URL + 'favorite'
      let myApp = this.$f7
      myApp.showIndicator()
      // let urldetail = url + routeparam
      axios.get(url)
        .then(response => {
          // JSON responses are automatically parsed.
          let res = response.data.data
          this.data = res
          // console.log(res)
          this.ready = true
          if (this.ready) {
            myApp.hideIndicator()
          }
        })
        .catch(e => {
          console.log('error')
          myApp.hideIndicator()
          this.$f7.alert('Network Error1')
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
        // console.log(this.cekopen)
      },
      redirect: function () {
        return this.$router.load({
          url: '/home/'
        })
      },
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
  /*height: 150px;*/
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
.content-block-title.title-tab {
  padding-top: unset !important;
  text-align: center;
  font-size: 18px !important;
}
</style>