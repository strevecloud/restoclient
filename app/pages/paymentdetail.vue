<template>
	<f7-page>
	<f7-navbar title="Detail Pembayaran" link="/" back-link="Back" sliding/>
	<div class="card data-table">
	  <table>
	    <thead>
	      <tr>
	        <th class="label-cell">Nama Menu</th>
	        <th class="numeric-cell">Qty</th>
	        <th class="numeric-cell">Harga</th>
	      </tr>
	    </thead>
	    <tbody>
	      <tr v-for="item in data">
	        <td class="label-cell">{{ item.name }}</td>
	        <td class="numeric-cell">{{ item.count }}</td>
	        <td class="numeric-cell">{{ totalItem }}{{ formatPrice(item.price) }}</td>
	        <span>{{ totalItem }}</span>
	      </tr>
	      <tr>
	      	<td class="label-cell">Sub Total</td>
	        <td colspan="2" class="numeric-cell">{{ formatPrice(subTotal) }}</td>
	      </tr>
	      <tr>
	      	<td class="label-cell">Tax</td>
	        <td colspan="2" class="numeric-cell">{{ formatPrice(totalPajak) }}</td>
	      </tr>
	      <tr class="total">
	      	<td class="label-cell">Total</td>
	        <td colspan="2" class="numeric-cell">{{ formatPrice(total) }}</td>
	      </tr>
	    </tbody>
	  </table>
	  <br>
	  <a href="#" @click="done" class="button button-raised button-pink">Done</a>
	</div>
	</f7-page>
</template>
<script>
  import Countdown from 'vuejs-countdown'
  import axios from 'axios'
  import * as CONFIG from '../config'
  export default {
    components: {
      Countdown
    },
    data () {
      return {
        data: [],
        total: 0,
        tax: 0,
        subTotal: 0,
        totalPajak: 0,
        ready: false
      }
    },
    created: function () {
      let userid = localStorage.getItem('userid')
      let url = CONFIG.URL + 'billing/' + userid
      let myApp = this.$f7
      myApp.showIndicator()
      axios.get(url)
        .then(response => {
          let res = response.data.data
          this.data = res
          this.ready = true
          this.tax = res[0].tax
          if (this.ready) {
            myApp.hideIndicator()
          }
        })
        .catch(e => {
          console.log(e)
          myApp.hideIndicator()
          // this.$f7.alert('Network Error')
        })
    },
    methods: {
      formatPrice (value) {
        let val = (value / 1).toFixed(2).replace('.', ',')
        return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
      },
      done: function () {
        let url = CONFIG.URL + 'setting'
        let userid = localStorage.getItem('userid')
        var formData = new FormData()
        formData.append('account', userid)
        axios.post(url, formData).then((response) => {
          window.f7.alert('Thank You')
          return this.$router.load({
            url: '/home/'
          })
        })
          .catch(e => {
            window.f7.alert('Sory Try Again Later')
          })
      }
    },
    computed: {
      totalItem: function () {
        Object.entries(this.data).forEach(([key, val]) => {
          let harga = parseInt(val.price)
          this.total += harga
        })
        let totalTax = (this.total * this.tax) / 100
        let totalAll = this.total + totalTax
        this.subTotal = this.total
        this.totalPajak = totalTax
        this.total = totalAll
        console.log(totalAll)
      }
    }
  }
</script>
<style type="text/css">
  tr.total {
    background-color: #dcdcdc5e;
  }
  a.button.button-raised.button-pink {
    background-color: #CC0D52 !important;
    color: white !important;
  }
</style>