<template>
  <transition appear appear-to-class="animated lightSpeedIn">
    <div class="index-wrap">
      <h2 class="lunar">农历十月初八</h2>
      <p class="title">欢迎收听中国民间故事</p>
      <div class="content-wrap">
        <h2 class="content-title">民间故事-半夜来的神秘美女</h2>
        <p class="desc">----故事由网友提供，喜欢的朋友请分享转发</p>
        <div id="content" class="content">某天，和施耐1111124457891邻而居的顾员庵比邻而居的顾员外来到他家，说儿子顾斐这些天卧床不起，想请施比邻而居的顾员外来耐庵前往诊视。施耐庵慨然应允，来到顾家后，只见顾公子年约二十，可是却面色萎黄，精神恍惚，脉象细涩而无力，看样子病得不轻。施耐庵便耐心地询问病情，而病者却闭目答非所问，口中只喃喃地念道：“此木为柴山山出。”施耐庵听后，心中颇觉奇怪，这分明是个上联嘛，难道公子只是苦于无对，方才……于是他便对顾公子说道：“有对了！”顾公子悠然睁开双眼333，只听施耐庵对道：“因火成烟夕夕多。”这分明是副绝对，顾公子一下子精神大振，竟坐起来喜道：“请问先生，‘山石岩前古木枯’，可有下对？”施耐庵略加思索，然后答道：“白水泉中日月明。</div>
      </div>
      <div class="btn-wrap">

      </div>
    </div>
  </transition>
</template>

<script>
import { log } from "util";
export default {
  data() {
    return {
      date: ""
    };
  },
  mounted() {
    var dt = document.querySelectorAll("[data-timeline]")[0];
    console.log(dt);
    console.log(document.getElementById("num").dataset.timeline);
    document.getElementById("num").className = "now";
    console.log(document.getElementsByClassName('content'));
    audio.addEventListener("timeupdate", function(e) {
      var time = parseInt(e.target.currentTime); //获取当前时间
      var lines = document.querySelectorAll("[data-timeline]");
      var top = 0;
      var _thisHeight = 0;
      var nextLine = {
        i: 0,
        time: 0
      };
      for (var i in lines) {
        var line = lines[i];
        if (line.dataset != undefined) {
          var timeline = parseInt(line.dataset.timeline);
          if (timeline == time) {
            _thisHeight = line.clientHeight; //将当前歌词高度记录
            line.className = "now";
            //获取下一句歌词
            nextLine.i = parseInt(i) + 1;
            try {
              nextLine.time = lines[nextLine.i].dataset.timeline;
            } catch (e) {}
            if (nextLine.time > 0) {
              var interval = nextLine.time - timeline;
              (function(k) {
                setTimeout(function() {
                  lines[k].className = "";
                }, interval * 1000);
              })(i);
            }
            document.querySelector(".lrc>.content").style.marginTop =
              -(top - _thisHeight) + "px";
          } else if (timeline < time) {
            top += line.clientHeight;
          }
        }
      }
    });
    // this.handleMark();
  },
  methods: {
    //#ed7d31

    handleMark() {
      var content = document.getElementById("content");
      var text = content.innerHTML; //整个字符串
      var len = text.length;
      var markLen = 10;
      var arrText = text.split(""); //整个数组
      var i = 0;
      var timer = setInterval(()=>{
        if(i>=len) {
          console.log('end'+i)
          content.innerHTML = text;
          clearInterval(timer);
        } else {
          var markValue = arrText.slice(i, i+markLen).join(""); // 被标记字符串
          var remainValue = text.split(markValue); //剩余数组
          content.innerHTML = remainValue.join('<span style="color:#ed7d31;">'+ markValue + "</span>");
          i+=1
        }
      },100)
    }
  }
};
</script>
<style lang="less" scoped>
.index-wrap {
  min-height: 100vh;
  width: 100%;
  // background-image: linear-gradient(-225deg, #231557 0%, #44107A 29%, #FF1361 67%, #FFF800 100%);
  background-color: #2b2324;
  color: #fff;
  padding: 0.3rem 0;
  .lunar {
    margin-left:0.3rem;
    font-size:18px;

  }
  .title {
    font-size:15px;
    margin-left:0.3rem;
    margin-top:0.15rem;
  }
  .content-wrap {
    margin-top:1rem;
    padding:0 0.36rem;
    font-size:18px;
    color:#a6a6a6;
    .content-title{
      color:#d9d9d9;
      font-size:28px;
      margin-bottom:.25rem;
    }
    .desc {
      font-size:14px;
      margin-bottom:.35rem;
      text-indent:2em;
    }
    .content {
      text-indent:2em;
      line-height: 30px;
    }
  }
  .btn-wrap {
    position: fixed;
    bottom:10px;
    left:50%;
    margin-left:-200px;
    width:400px;
  }
}
</style>
