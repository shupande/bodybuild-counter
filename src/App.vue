<template>
    <div id="app">
        <mt-header fixed title="健身计数器">
          <router-link to="/" @click="reset" slot="left">
              <img class="reset" src="./assets/images/reset.png">
          </router-link>
          <mt-button icon="more" @click.native="popupVisible = true"  slot="right"></mt-button>
        </mt-header>
        <mt-popup v-model="popupVisible"  position="right" class="mint-popup-3" :modal="true">
            <div class="about">
              <h2>健身计数器</h2>
              <div class="guide">
                <p>使用方法：</p>
                <p>1)做俯卧撑时使用鼻子触控。</p>
                <p>2)仰卧起坐或者卷腹时用手肘触控。</p>
                <p>3)平板支撑直接点击开始计时即可。</p>
              </div>
              <br>
              <p>受万恶的美帝电影影响，男女都对大胸部深有喜爱，经过老衲一番Google选出了练就大胸Ji和减肚子的三大方法。</p>
              <br>
              <p>由于练习时心里默数会导致分神，遂产生本想法，算是学习VueJs和Cordova的练手。</p>
              <h3>by @舒盼unimz</h3>
              <mt-button @click.native="popupVisible = false" size="large" type="primary">
              朕知道了</mt-button>
            </div>
        </mt-popup>
        <div v-on:click="count">
            <h1>{{counter}}</h1>
            <div v-bind:class="sw"></div>
            <audio v-bind:src="soundsrc" autoplay v-if="autoplay">
        </div>
        <mt-tabbar v-model="selected">
            <mt-tab-item id="push-up">
                <img slot="icon" src="./assets/images/push-up.png"> 俯卧撑
            </mt-tab-item>
            <mt-tab-item id="sit-ups">
                <img slot="icon" src="./assets/images/sit-ups.png"> 仰卧起坐
            </mt-tab-item>
            <mt-tab-item id="plank">
                <img slot="icon" src="./assets/images/plank.png"> 平板支撑
            </mt-tab-item>
        </mt-tabbar>
    </div>
</template>
<script>
// 全局定时器变量
var n= 0, timer=null;

export default {
    data() {
            return {
                sw: 'switch-off',
                soundsrc: "../static/sound/ring.wav",
                counter: "0.00",
                autoplay: false,
                selected: '',
                popupVisible: false
            }
        },
        methods: {
            count: function() {
                var that = this;
                if (this.sw == 'switch-on') {
                    this.sw = 'switch-off';
                    this.autoplay = false;
                    clearInterval(timer);
                } else {
                    this.sw = 'switch-on';
                    this.autoplay = true;
                    //计时器
                    timer=setInterval(function () {
                      n++;
                      var m=parseInt(n/60);
                      var s=parseInt(n%60);
                      //毫秒不足10补0
                      if(s<10) s="0"+s;
                      that.counter=m+"."+s;
                    },1000/60);
                }

            },
            reset: function() {
                clearInterval(timer);
                this.counter = "0.00";
                n=0;
                this.sw = 'switch-off';
            }
  }
}
</script>
<style>
html {
    height: 100%;
    background-color: #EAEAEA;
}
h1 {
    font-size: 5em;
    margin: 50px 0px 50px 0px;
}
p {
    display: block;
    -webkit-margin-before: 0em;
    -webkit-margin-after: 0em;
    -webkit-margin-start: 0px;
    -webkit-margin-end: 0px;
}
#app {
    color: #2c3e50;
    font-family: 微软雅黑, Source Sans Pro, Helvetica, sans-serif;
    text-align: center;
}
.switch-on {
    width: 178px;
    height: 178px;
    margin: 0 auto;
    background-image: url("assets/images/on.png");
    background-repeat: no-repeat;
    background-origin: padding-box;
    background-position: center;
    background-size: cover;
}

.switch-off {
    width: 178px;
    height: 178px;
    margin: 0 auto;
    background-image: url("assets/images/off.png");
    background-repeat: no-repeat;
    background-origin: padding-box;
    background-position: center;
    background-size: cover;
}
.reset{
    width: 20px;
    height: 20px;
}
.mint-popup-3 {
    width: 100%;
    height: 100%;
    background-color: #fff;
    opacity: 0.9;
}
.about{
    display: flex;
    flex-direction:column;
    justify-content:center;
    padding: 10px;
}
.guide{
  text-align: left;
  margin:0 auto;
}
.mint-popup-3 .mint-button {
    width: 30%;
    margin: 0 auto;
}
/*禁止长按复制*/

* {
    -webkit-touch-callout: none;
    /* prevent callout to copy image, etc when tap to hold */
    -webkit-text-size-adjust: none;
    /* prevent webkit from resizing text to fit */
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
    /* make transparent link selection, adjust last value opacity 0 to 1.0 */
    -webkit-user-select: none;
    /* prevent copy paste, to allow, change 'none' to 'text' */
}
</style>
