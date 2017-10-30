<template>
<f7-page>
<f7-navbar title="Inprogress" link="/" back-link="Back" sliding/>
<div class="list-block">
  <ul>
    <li>
      <a href="#" class="item-link item-content">
        <div class="item-media"><i class="icon icon-f7"></i></div>
        <div class="item-inner">
          <div class="item-title">Miayam</div>
          <div id="countdown" class="item-after">{{ displaytime }}
          </div>
        </div>
      </a>
    </li>
    <li>
      <a href="#" class="item-link item-content">
        <div class="item-media"><i class="icon icon-f7"></i></div>
        <div class="item-inner">
          <div class="item-title">Bakso</div>
          <div class="item-after">{{ displaytime }}</div>
        </div>
      </a>
    </li>
    <li>
      <a href="#" class="item-link item-content">
        <div class="item-media"><i class="icon icon-f7"></i></div>
        <div class="item-inner">
          <div class="item-title">Soto</div>
          <div class="item-after">{{ displaytime }}</div>
        </div>
      </a>
    </li>
  </ul>
</div>
</f7-page>
</template>
<script type="text/javascript">
var count = 0
var counter = null
var inputMinute = 1
export default {
  data: function () {
    return {
      details: [],
      titles: '',
      minute: '',
      hour: '',
      second: '',
      displaytime: ''
    }
  },
  created: function () {
    this.initCounter(inputMinute)
  },
  methods: {
    initCounter: function (minute) {
      var tominute = (minute * 60)
      count = this.getLocalStorage('count') || tominute
      counter = setInterval(this.timer, 1000)
    },
    setLocalStorage: function (key, val) {
      if (window.localStorage) {
        window.localStorage.setItem(key, val)
      }
      return val
    },
    getLocalStorage: function (key) {
      return window.localStorage ? window.localStorage.getItem(key) : ''
    },
    timer: function () {
      count = this.setLocalStorage('count', count - 1)
      var seconds = count % 60
      var minutes = Math.floor(count / 60)
      var hours = Math.floor(minutes / 60)
      minutes %= 60
      hours %= 60
      this.hour = hours
      this.minute = minutes
      this.second = seconds
      this.display(hours, minutes, seconds)
      if (count === -1) {
        clearInterval(counter)
        this.displaytime = 'Done'
      }
    },
    display: function (h, m, s) {
      this.displaytime = (h + ': ' + m + ': ' + s)
    }
  }
}
</script>