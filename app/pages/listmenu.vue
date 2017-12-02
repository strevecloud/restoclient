<template>
	<f7-page>
		<f7-navbar title="Menu" link="/" back-link="Back" sliding/>
		<!-- <f7-toolbar tabbar bottom>
		<div class="toolbar-inner">
		<a href="#tab1" class="tab-link">
            <i class="f7-icons">home</i>
            <span class="tabbar-label">Home</span>
        </a>
        <a href="/menusquare" class="toolbar-link">
            <i class="f7-icons">data</i>
            <span class="toolbar-label">Grid</span>
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
		<div class="list-block media-list">
		  <ul>
		    <li v-for="n in 8">
		      <a href="/detailmenu" class="item-content list">
		        <div class="item-media image-square"><img src="http://rasasayange.co.id/assets/images/large_resep_85_mie%20ayam%202.jpg"></div>
		        <div class="item-inner item-list">
		          <div class="item-title-row">
		            <div class="item-title title-list">Yellow Submarine</div>
		            <!-- <div class="item-after">$15</div> -->
		          </div>
		          <div class="item-text text-description">Lorem ipsum dolor sit amet...</div>
		          <!-- <div class="item-subtitle">Beatles</div> -->
		        </div>
		      </a>
		    </li>
		  </ul>
		</div>
	</f7-page>
</template>
<style type="text/css">
.item-media.image-square img{
    display: block;
    width: 40vw;
    padding-top: unset !important;
    border-radius: 5px;
}
.item-media.image-square{
    padding-top: 7px !important;
    padding-bottom: 7px !important;
}
.list-block .item-content.list{
	padding-left: 7px;
}
.item-inner.item-list{
	padding: unset!important;
	    margin: auto;
    margin-left: 4%;
}
.item-title.title-list{
	/*padding-top: 7px;*/
	color: #6e6e6e;
}
.item-text.text-description{
	font-size: 8px !important;
}
.tabbar a.tab-link, .tabbar a.link {
	text-transform:unset !important;
	padding-top: 8px !important;
}
a.toolbar-link {
    display: inline-grid;
    padding-top: 8px;
    color: rgba(255, 255, 255, 0.7) !important;
    width: 100%;
 }
 span.toolbar-label {
    margin: auto;
}
</style>