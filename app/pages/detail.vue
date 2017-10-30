<template>
<f7-page>
     <f7-navbar :title="title" link="/" back-link="Back" sliding/>
    <div class="content-block-title">Detail Menu</div>
    <div class="card demo-card-header-pic">
        <div :style="{ 'background-image': 'url(' + imagefood + ')' }" valign="bottom" class="card-header color-white no-border">{{ namefood }}</div>
        <div class="card-content">
            <div class="card-content-inner">
                <p class="color-gray">{{ namefood}}</p>
                <p class="color-gray">Harga : {{ formatPrice(pricefood)}}</p>
                <p class="color-gray">Lama Pembuatan : {{ timefood }} Menit</p>
                <p>{{ descriptionfood }}</p>
                
            </div>
        </div>
        <div class="card-footer">
            <a href="#" class="link">Favorite</a>
            <a href="/inprogress" class="link">Buy</a>

        </div>
    </div>
</f7-page>
</template>

		<style>
  .demo-card-header-pic .card-header {
    height: 50vw;
    background-size: cover;
    background-position: center;
  }
</style>
<script type="text/javascript">
  import axios from 'axios'
  import * as CONFIG from '../config'
export default {
    data: function () {
      return {
        details: [],
        title: '',
        namefood: '',
        descriptionfood: '',
        imagefood: '',
        pricefood: '',
        timefood: ''
      }
    },
    created: function () {
      let routeparam = this.$route.params.id
      this.title = this.$route.params.name
      // console.log(routeparam)
      // let urldetail = '../json/resto' + routeparam + '.json'
      let url = CONFIG.URL + 'menu/'
      let urldetail = url + routeparam
      axios.get(urldetail)
        .then(response => {
          // JSON responses are automatically parsed.
          let res = response.data
          this.details = res
          this.title = res.name
          this.namefood = res.name
          this.descriptionfood = res.description
          this.imagefood = res.image
          this.pricefood = res.price
          this.timefood = res.time
          console.log(urldetail)
        })
        .catch(e => {
          alert(e)
          console.log('error')
        })
    },
    methods: {
      formatPrice (value) {
        let val = (value / 1).toFixed(2).replace('.', ',')
        return 'Rp ' + val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
      }
    }
}
</script>