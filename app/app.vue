<template>
  <div id="app">
    <!-- <login-popup /> -->
    <f7-views>
      <f7-view main url="/home/" navbar-through :dynamic-navbar="$theme.ios" />
    </f7-views>
  </div>
</template>
<style type="text/css">
	.navbar-fixed .navbar, .navbar-through .navbar{
  box-shadow: none;
}
</style>
<script type="text/javascript">
  export default {
    mounted: function () {
      document.addEventListener('backbutton', onBackKeyDown, false)

      function onBackKeyDown (e) {
        this.$f7.views.main.router.back()
      }
    }
  }
</script>