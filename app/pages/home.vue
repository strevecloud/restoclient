<template>
  <f7-page v-if="!status">
  <f7-navbar :title="$root.config.title" :dynamic-navbar="true" main/>
    <f7-block-title>Welcome</f7-block-title>
    <div class="row">
    	<div class="col-50 tablet-25">
    		<div class="card">
			  <div class="card-content">
			    <div class="card-content-inner">
			    	<a href="/menumakanan"><img src="../images/menures.svg"></a>
			    </div>
			  </div>
			  <div class="card-footer">All Menu</div>
			</div>
    	</div>
    	<div class="col-50 tablet-25">
    		<div class="card">
			  <div class="card-content">
			    <div class="card-content-inner">
			    	<a href="/category"><img src="../images/restaurant.svg"></a>
			    </div>
			  </div>
			  <div class="card-footer">Menu Category</div>
			</div>
    	</div>
    	<div class="col-50 tablet-25">
    		<div class="card">
			  <div class="card-content">
			  	<a href="/paymentdetail">
			    <div class="card-content-inner">
			    	<img src="../images/restaurant-membership-card-tool.svg">
			    </div>
			    </a>
			  </div>
			  <div class="card-footer">Detail Payment</div>
			</div>
    	</div>
    	<div class="col-50 tablet-25">
    		<div class="card">
			  <div class="card-content">
			    <div class="card-content-inner">
			    	<img src="../images/chef.svg">
			    </div>
			  </div>
			  <div class="card-footer">Call Waiters</div>
			</div>
    	</div>
    </div>
    <div class="row">
    	<div class="col-50 tablet-25">
    		<div class="card">
			  <div class="card-content">
			    <div class="card-content-inner">
			    	<img src="../images/cup-black-silhouette.svg">
			    </div>
			  </div>
			  <div class="card-footer">Drink</div>
			</div>
    	</div>
    	<div class="col-50 tablet-25">
    		<div class="card">
			  <div class="card-content">
			    <div class="card-content-inner">
			    	<img src="../images/teacarrying.svg">
			    </div>
			  </div>
			  <div class="card-footer">More Order</div>
			</div>
    	</div>
    	<div class="col-50 tablet-25">
    		<div class="card">
			  <div class="card-content">
			    <div class="card-content-inner">
			    	<img src="../images/restaurant-table-and-chairs.svg">
			    </div>
			  </div>
			  <div class="card-footer">Proggress</div>
			</div>
    	</div>
    	<div class="col-50 tablet-25">
    		<div class="card">
			  <div class="card-content">
			    <div class="card-content-inner">
			    	<img src="../images/food-covered-tray-silhouette.svg">
			    </div>
			  </div>
			  <div class="card-footer">Done</div>
			</div>
    	</div>
    </div>
  </f7-page>
  <f7-page v-else="status">
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
                        <input type="text" name="username" placeholder="Username">
                      </div>
                    </div>
                  </li>
                  <li class="item-content">
                    <div class="item-inner">
                      <div class="item-title label">Password</div>
                      <div class="item-input">
                        <input type="password" name="password" placeholder="Password">
                      </div>
                    </div>
                  </li>
                </ul>
              </div>
              <div class="list-block">
                <ul>
                  <li class="content-block">
                    <a href="#" class="button" @click="login">Sign In</a>
                  </li>
                </ul>
                <div class="list-block-label">Please Signin.</div>
              </div>
            </form>
          </div>
        </div>
  </f7-page>
</template>
<style type="text/css">
	.navbar-fixed .navbar, .navbar-through .navbar{
  box-shadow: none;
  }
.popup-overlay.modal-overlay-visible {
    visibility: hidden;
}
	div[class*="col-"] {
  background: #fff;
  text-align: center;
  color: #000;
  /*border: 1px solid #ddd;*/
  padding: 5px;
}
.row {
  margin-bottom: 15px;
}        
</style>
<script type="text/javascript">
    export default {
      data () {
        return {
          cekopen: true,
          status: true,
          name: '',
          password: ''
        }
      },
      created: function () {},
      methods: {
        login: function () {
          console.log('login')
          this.cekopen = false
          this.status = false
        },
        logout: function () {
          console.log('logout')
          this.cekopen = true
          this.status = true
        }
      }
    }
</script>