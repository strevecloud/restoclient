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
	      <tr>
	        <td class="label-cell">Mcd Paket Jumbo</td>
	        <td class="numeric-cell">2</td>
	        <td class="numeric-cell">114.000</td>
	      </tr>
	      <tr>
	        <td class="label-cell">Sate Kambing Muda</td>
	        <td class="numeric-cell">1</td>
	        <td class="numeric-cell">108.000</td>
	      </tr>
	      <tr class="total">
	      	<td class="label-cell">Total</td>
	        <td colspan="2" class="numeric-cell">222.000</td>
	      </tr>
	    </tbody>
	  </table>
	</div>
	</f7-page>
</template>
<style type="text/css">
	tr.total {
    background-color: #dcdcdc5e;
}
</style>