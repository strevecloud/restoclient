<template>
<f7-page>
     <f7-navbar :title="title" link="/" back-link="Back" sliding/>
    <!-- <div class="content-block-title">Detail Menu</div> -->
    <div v-if="ready" class="card demo-card-header-pic">
        <div v-if="imagefood" :style="{ 'background-image': 'url(' + imagefood + ')' }" valign="bottom" class="card-header color-white no-border"></div>

        <div v-if="!imagefood" valign="bottom" class="card-header color-white no-border" style="background-image: url('../images/no-image.svg');"></div>
        <div class="card-content">
            <div class="card-content-inner">
                <p class="color-black">{{ namefood}}</p>
                <p class="color-gray">Harga : {{ formatPrice(pricefood)}}</p>
                <p class="color-gray">Lama Pembuatan : {{ timefood }} Menit</p>
                <p>{{ descriptionfood }}</p>
                
            </div>
        </div>
        <div class="card-footer">
            <div class="buynow">
              <i class="fa fa-minus-square fa-lg" @click="kurang" aria-hidden="true"></i>
              <input type="number" name="qty" class="inputinline" :value="counter" readonly>
              <i class="fa fa-plus-square fa-lg" @click="tambah" aria-hidden="true"></i>
            </div>
            <a href="/inprogress" class="link">Order</a>

        </div>
        <form class="list-block inputs-list" v-if="isMorethanZero">
        <ul>
        <li>
        <!-- <div class="card-footer"> -->
         <div class="item-content">
            <div class="item-inner">
               <div class="item-input item-input-field">
                  <textarea type="text" placeholder="Catatan" class="resizable"></textarea>
               </div>
            </div>
         </div>
      <!-- </div> -->
    </li>
  </ul>
</form>

    </div>

</f7-page>
</template>

		<style>
  .demo-card-header-pic .card-header {
    height: 50vw;
    background-size: cover;
    background-position: center;
  }
  .inputinline{
    width: 40px;
    height: 16px;
    margin-left: 1px;
    margin-right: 1px;
    /*margin-bottom: 3px;*/
    text-align: center;
  }
.fa-minus-square:before {
    content: "\F146";
    font-size: 30px;
}
.fa-plus-square:before {
    content: "\F0FE";
    font-size: 30px;
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
        timefood: '',
        counter: 0,
        ready: false,
        isMorethanZero: false
      }
    },
    created: function () {
      let routeparam = this.$route.params.id
      this.title = this.$route.params.name
      // console.log(routeparam)
      // let urldetail = '../json/resto' + routeparam + '.json'
      let url = CONFIG.URL + 'item/'
      let urldetail = url + routeparam
      let myApp = this.$f7
      myApp.showIndicator()
      axios.get(urldetail)
        .then(response => {
          // JSON responses are automatically parsed.
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
          // console.log(pricefood)
        })
        .catch(e => {
          alert(e)
          console.log('error')
        })
    },
    methods: {
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
      }
    }
}
</script>