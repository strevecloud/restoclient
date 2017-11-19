<template>
<f7-page>
<f7-navbar title="Inprogress" link="/" back-link="Back" sliding/>
<div class="content-block-title">Inprogress</div>
<div class="list-block">
  <ul>
    <Countdown name="Mie Ayam" status="status" deadline="2017-11-18 18:13:00"></Countdown>
  </ul>
</div>
</f7-page>
</template>
<script>
import Countdown from 'vuejs-countdown'

export default {
  components: { Countdown }

}
</script>