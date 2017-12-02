<template>
	<f7-page>
		<f7-navbar title="Menu" link="/" back-link="Back" sliding/>
<!-- 		<f7-toolbar tabbar bottom>
		<div class="toolbar-inner">
		<a href="#tab1" class="tab-link">
            <i class="f7-icons">home</i>
            <span class="tabbar-label">Home</span>
        </a>
        <a href="/listmenu" class="toolbar-link">
            <i class="f7-icons">menu</i>
            <span class="toolbar-label">List</span>
        </a>
        <a href="#tab2" class="tab-link">
             <i class="f7-icons">star</i>
            <span class="tabbar-label">Favorite</span>
        </a>
        <a href="/categorynew" class="toolbar-link">
            <i class="f7-icons">book</i>
            <span class="toolbar-label">Menu</span>
        </a>
    </div>
		</f7-toolbar> -->
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