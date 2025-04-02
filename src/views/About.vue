<template>
  <div class="about" @mouseup="handleMouseUp">
    <div id="pannellum"></div>
    <div class="map-container">
      <img 
        :style="baseImgCss" 
        :class="{fullsize: showPicture}" 
        :src="mapImg" 
        alt="map" 
        @click="showPicture = false"
      >
    </div>
  </div>
</template>
<script>
import 'pannellum/build/pannellum.css';
import 'pannellum/build/pannellum.js';

export default {
  name: 'VrCubaAbout',
  data() {
    return {
      viewer: null,
      showPicture: false,
      originX: 0,
      originY: 0,
      mapImg: require('@/assets/map.jpg')
    }
  },
  computed: {
    baseImgCss() {
      return {
        left: this.originX,
        top: this.originY
      }
    }
  },
  methods: {
    handleMouseUp(e) {
      this.$nextTick(() => {      
        if (!this.showPicture && this.viewer) {
          // cssClass自定义的classname在此拿不到dom~
          const str = document.querySelector('.pnlm-hotspot-base').style.transform.split('translate')[1];
          const arr = str.split('(')?.[1].split(')')?.[0].split(',').map(item => item.trim());
          if(arr.length === 2) {
            const [clientX, clientY] = arr
            this.originX = clientX;
            this.originY = clientY;
          }
        }
      });
    }
  },
  mounted() {
    const that = this;
    this.$nextTick(() => {
      this.viewer = window.pannellum.viewer('pannellum', {
        type: "cubemap",
        autoLoad: true,
        showFullscreenCtrl: false, // 隐藏全屏按钮 否则全屏时藏宝图弹出层级低 看不见
        cubeMap: Array.from({length: 6}, (_, i) => require(`@/assets/room${i}.jpg`)),
        hotSpots: [
          {
            pitch: 1,
            yaw: -138,
            type: "info",
            text: "树洞藏宝图",
            clickHandlerFunc: function(e) {
              that.$nextTick(() => {
                that.showPicture = true;
              });
            },
            // cssClass: "holo pnlm-hotspot pnlm-sprite pnlm-info",
          },
        ]
      })
    });
  },
};
</script>
<style scoped lang="scss">
  .about {
   width: 100%;
   height: 100%;
   position: relative;
   #pannellum {
     width: 100%;
     height: 100%;
   }
   .map-container {
     position: absolute;
     top: 0;
     left: 0;
     top: 0;
     bottom: 0;
     display: flex;
     width: 100vw;
     height: 100vh;
     pointer-events: none;
     img {
       position: absolute;
       width: 0;
       height: 0;
       transition: all 1s;
       pointer-events: visible;
       &.fullsize {
        left: 0 !important;
        top: 0 !important;
        width: 100vw;
        height: 100vh;
       }
     }
   }

 }
</style>
