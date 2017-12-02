<template>
	<f7-page>
		<f7-navbar title="Home" link="/" back-link="Back" sliding/>
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
          <div class="col-50 padding-square" v-for="n in 6">
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
          <div class="col-50 padding-square" v-for="n in 6">
            <a href="/detailmenu">
            <div class="card demo-card-header-pic">
          <div style="background-image:url('https://skounis.s3.amazonaws.com/mobile-apps/restaurant-ionic/_demonstration/assets/cat-a-1-1.png')" valign="bottom" class="square"></div>
          <div class="card-content">
            <div class="card-content-inner text">
              <h3 class="single-title-menu">Cretan Ntakos</h3>
              <h4 class="single-title-menu">Rp 34.000</h4>
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
</template>
<script>
  import Vue from 'vue'
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
        }
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