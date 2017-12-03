<template>
	<f7-page>
	<f7-navbar :title="title" link="/" back-link="Back" sliding/>
		<div class="card demo-card-header-pic single">
		  <div style="background-image:url('http://rasasayange.co.id/assets/images/large_resep_85_mie%20ayam%202.jpg')" class="card-header"></div>
		  <div class="card-content">
		    <div class="card-content-inner single">
		    	<div class="col-50 col-detail-menu">
		    		<h3 class="single-title grey">{{ namefood}}</h3>
		    		<div class="description-grey">Mi ayam atau bakmi ayam adalah masakan Indonesia yang terbuat dari mi kuning direbus mendidih kemudian ditaburi saos kecap khusus beserta daging ayam dan sayuran. Mi Ayam terkadang ditambahi dengan bakso, pangsit dan jamur.</div>
		    		<h4 class="single-title grey">Informasi</h4>
		    		<div class="list-block">
				      <ul class="list-block">
				        <li class="item-content">
				          <div class="item-media"><i class="f7-icons">card</i></div>
				          <div class="item-inner">
				            <div class="item-title">Harga</div>
				            <div class="item-after">{{ formatPrice(pricefood)}}</div>
				          </div>
				        </li>
				        <li class="item-content">
				          <div class="item-media"><i class="f7-icons">time</i></div>
				          <div class="item-inner">
				            <div class="item-title">Waktu</div>
				            <div class="item-after">{{ timefood }} Menit</div>
				          </div>
				        </li>
				      </ul>
				  </div>
		    	</div>
		    	<p class="buttons-row">
					  <a @click="buy" href="#" class="button button-fill button-raised pink">
					  	<i class="fa fa-shopping-cart" aria-hidden="true"></i> Beli</a>
				  </p>     
		    </div>
		  </div>
		</div>
	  <div class="picker-modal">
	    <div class="toolbar">
	      <div class="toolbar-inner">
	        <div class="left"></div>
	        <div class="right button"><a href="#" @click="order" class="close-picker button color-white border-white">Done</a></div>
	      </div>
	    </div>
	    <div class="picker-modal-inner">
	    	<div class="list-block">
		      <ul>
		        <li>
		          <div class="item-content">
		          	<span class="item-inner auto">
                <a href="#" @click="kurang" class="disable-animation-button"><i class="f7-icons">delete_round</i></a>
            		<input type="text" class="qty" :value="counter" readonly>
            		<a href="#" @click="tambah" class="disable-animation-button"><i class="f7-icons">add_round</i></a>
            		</span>
		          </div>
		        </li>
		        <li>
			      <div class="item-content">
			        <div class="item-inner">
			          <span class="inline-block">
			            <textarea placeholder="Catatan" v-model="note" cols="100%"></textarea>
			          </span>
			        </div>
			      </div>
			    </li>
		    </ul>
			</div>
	    </div>
	  </div>
	</f7-page>
</template>
<script type="text/javascript">
 import axios from 'axios'
 import * as CONFIG from '../config'
 export default {
   data: function () {
     return {
       data: [],
       counter: 0,
       isMorethanZero: false,
       details: [],
       title: '',
       namefood: '',
       descriptionfood: '',
       imagefood: '',
       pricefood: '',
       timefood: '',
       ready: false,
       note: '',
       idmenu: 0
     }
   },
   created: function () {
     let myApp = this.$f7
     this.$$(document).on('page:back', function (e) {
       myApp.closeModal('.picker-modal')
     })
     let routeparam = this.$route.params.id
     this.idmenu = routeparam
     this.title = this.$route.params.name
     let url = CONFIG.URL + 'item/'
     let urldetail = url + routeparam
     myApp.showIndicator()
     axios.get(urldetail)
       .then(response => {
         let res = response.data.data[0]
         this.details = res.data
         this.title = res.name
         this.namefood = res.name
         this.descriptionfood = res.description
         this.imagefood = res.image
         this.pricefood = res.price
         this.timefood = res.time
         this.ready = true
         if (this.ready) {
           myApp.hideIndicator()
         }
       })
       .catch(e => {
         alert(e)
         console.log('error')
       })
   },
   methods: {
     buy: function () {
       let myApp = this.$f7
       myApp.pickerModal('.picker-modal')
     },
     formatPrice (value) {
       let intHarga = parseInt(value)
       let val = (intHarga / 1).toFixed(2).replace('.', ',')
       return 'Rp ' + val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
     },
     tambah: function () {
       this.counter += 1
       this.isMorethanZero = true
     },
     kurang: function () {
       if (this.counter === 0) {
         this.isMorethanZero = false
         this.counter = 0
       } else {
         this.counter -= 1
         if (this.counter === 0) {
           this.isMorethanZero = false
         }
       }
     },
     order: function () {
       if (this.counter !== 0) {
         let url = CONFIG.URL + 'item'
         let userid = localStorage.getItem('userid')
         var formData = new FormData()
         formData.append('account', userid)
         formData.append('dish', this.idmenu)
         formData.append('note', this.note)
         formData.append('qty', this.counter)
         axios.post(url, formData).then((response) => {
           console.log(response)
           window.f7.alert('Thank You For Ordering')
           this.counter = 0
           this.note = ''
         })
           .catch(e => {
             window.f7.alert('Sory Try Again Later')
           })
       }
     }
   }
 }
</script>
<style type="text/css">
.card.demo-card-header-pic.single {
    background-color: #F5F5F5;
    box-shadow: none;
}
.card-content-inner.single {
    padding: 0px;
}
.demo-card-header-pic .card-header {
    height: 65vw;
    background-size: cover;
    background-position: center;
  }
  h3{
  	font-size: 24px;
  }
  h4{
  	font-size: 18px;
  }
 .single-title.grey{
 	font-weight: 500;
 	font-family: "-apple-system","Helvetica Neue",Roboto,"Segoe UI",sans-serif;
 	color: #6e6e6e;
  	text-align: left;
 	margin: 5px 0 5px 0;
  }
  .description-grey{
  	color: #6e6e6e;
  	text-align: left;
  	margin: 5px 0 5px 0;
  }
  .toolbar-inner{
  	background: #CC0D52 !important;
  }
  .picker-modal{
  	height: 160px !important;
  	/*background-color: #F5F5F5!important;*/
  }
  a.close-picker.button.color-white.border-white{
  	border-color: white;
    border: 1px solid;
  }
  .right.button{
  	margin-right: 5px;
  }
  input.qty {
    border: 1px solid black !important;
    height: 28px !important;
    width: 48px !important;
    text-align: center;
}
.item-inner.auto{
	width: unset !important;
	/*position: absolute !important;*/
    margin: auto !important;
    /*left: 26%;*/
}
span.inline-block {
    display: inherit;
}
.disable-animation-button{
  margin-left: 20px;
  margin-right: 20px;
}
/*.page-content{
	height: 350%!important;
}*/
</style>
