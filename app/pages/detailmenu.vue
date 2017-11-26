<template>
	<f7-page>
	<f7-navbar title="Menu" link="/" back-link="Back" sliding/>
		<div class="card demo-card-header-pic single">
		  <div style="background-image:url('http://rasasayange.co.id/assets/images/large_resep_85_mie%20ayam%202.jpg')" class="card-header"></div>
		  <div class="card-content">
		    <div class="card-content-inner single">
		    	<div class="col-50">
		    		<h3 class="single-title grey">Mie Ayam</h3>
		    		<div class="description-grey">Mi ayam atau bakmi ayam adalah masakan Indonesia yang terbuat dari mi kuning direbus mendidih kemudian ditaburi saos kecap khusus beserta daging ayam dan sayuran. Mi Ayam terkadang ditambahi dengan bakso, pangsit dan jamur.</div>
		    		<h4 class="single-title grey">Informasi</h4>
		    		<div class="list-block">
				      <ul class="list-block">
				        <li class="item-content">
				          <div class="item-media"><i class="f7-icons">card</i></div>
				          <div class="item-inner">
				            <div class="item-title">Harga</div>
				            <div class="item-after">Rp 14.000</div>
				          </div>
				        </li>
				        <li class="item-content">
				          <div class="item-media"><i class="f7-icons">time</i></div>
				          <div class="item-inner">
				            <div class="item-title">Waktu</div>
				            <div class="item-after">10 Menit</div>
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
	</f7-page>
</template>
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
</style>
<script type="text/javascript">
  export default {
    data: function () {
      return {
        data: []
      }
    },
    methods: {
      buy: function () {
        let myApp = this.$f7
        myApp.prompt('Jumlah?', function (value) {
          myApp.alert('Your name is "' + value + '". You clicked Ok button')
        })
      }
    }
  }
</script>