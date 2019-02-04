<template>
  <div id="wrapper">
    <div>
      <div class="voxy">
        <img id="voxy" src="../assets/voxy.png" width="30%" />
      </div>
      <div class="crown">
        <img id="crown" src="../assets/crown.png" width="30%"/>
      </div>
    </div>
      <h1>{{text}}</h1>
      <div v-if=game>
        <v-btn v-if=back @click="start()">バック開始</v-btn>
        <v-btn v-else @click="stop()">STOP</v-btn>
      </div>
      <div v-else>
        <v-btn @click="reload()">もう1回</v-btn>
      </div>
  </div>
</template>

<script>

export default {
  name: 'Voxy',
  data () {
    return {
      back: true,
      game: true,
      start_time: 0,
      finish_time: 0,
      text: '',
      distance: 0,
      spent: 0
    }
  },
  methods: {
    start () {
      this.start_time = Date.now()
      this.back = false
    },
    stop () {
      // 全体をz方向に動かす#scaler要素を取得
      this.finish_time = Date.now()
      let spent = this.finish_time - this.start_time
      let crown = document.getElementById('crown')
      let crownRect = crown.getBoundingClientRect()
      let voxy = document.getElementById('voxy')
      let voxyRect = voxy.getBoundingClientRect()
      this.distance = (voxyRect.x - spent / 10) - crownRect.x - crownRect.width
      voxy.style.transform = 'translateX(' + -spent / 10 + 'px)'
      voxy.style.transitionDuration = 3 + 's'
      setTimeout(this.result, 3000)
      this.game = false
    },
    result () {
      if (this.distance < 0) {
        let crown = document.getElementById('crown')
        crown.style.transform = 'rotate(-1080deg)'
        crown.style.transitionDuration = 1.5 + 's'
        this.text = '残念！あなたはクラウンにぶつけてしまいました'
      } else {
        this.text = 'あと' + this.distance / 10 + 'cmの余裕があります'
      }
    },
    reload () {
      location.reload()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
  margin: 0;
  padding: 0;
}
#wrapper {
  background-color: aliceblue;
  position: relative;
  width: 100%;
}

#wrapper:before {
  content: "";
  display: block;
  padding-top: 30%; /* 高さを幅の75%に固定 */
}

.voxy {
  text-align: right;
  padding-right: 2%;
  padding-top: 30px;
  position: absolute;
  top: 0px;
  right: 0;
  float: left;
  z-index: 100;
}

.crown {
  text-align: left;
  padding-left: 2%;
  padding-top: 30px;
  position: absolute;
  top: 15px;
  left: 0;
}
</style>
