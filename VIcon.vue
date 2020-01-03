<template lang="pug">

  div.v-icon.width_100.height_100(
    :style="iconStyle"
  )

</template>

<script>

export default {
  name: 'v-icon',
  props: {
    icon: String,
    mask: {
      type: Boolean,
      default: true
    }
  },
  data(){
    return {

    }
  },
  computed: {
    iconURL(){
      let iconPath;
      
      try {
        iconPath = require("assets/icons/" + this.icon);
      } catch(error) {
        if(process.env.NODE_ENV !== 'production'){
          window.console.error(`Icon ${this.icon} not found`);
        }
        iconPath = false;
      }
      
      return iconPath;
    },
    iconStyle(){
      let iconStyle;

      if (this.iconURL) {
        iconStyle = {
          'mask-image': `url(${this.iconURL})`,
        } 
      } else if(process.env.NODE_ENV !== 'production') {
        iconStyle = {
          'border': '2px solid red',
          'background-image': 'repeating-linear-gradient(-45deg, rgba(0,0,0,0.75) 0%, rgba(0,0,0,0.75) 10%, rgba(255,220,0,0.75) 10%, rgba(255,220,0,0.75) 20%)'
        } 
      }

      return iconStyle;
    },
    iconClass(){
      return {
        'v-icon_masked': this.mask
      }
    }
  }
}

</script>

<style lang="scss">

.v-icon{
  background-color: currentColor;

  background-origin: border-box;
  background-repeat: no-repeat;
  background-size: contain;
  background-position-y: center;
  background-position-x: center;


  &.v-icon_masked{
    mask-origin: border-box;
    mask-repeat: no-repeat;
    mask-size: contain;
    // mask-position-y: center;
    -webkit-mask-position-y: center;
    // mask-position-x: center;
    -webkit-mask-position-x: center;
  }

  &_h{
    &_t{
      background-position-y: top;
      // mask-position-y: top;
      -webkit-mask-position-y: top;
    }
    &_c{
      background-position-y: center;
      // mask-position-y: center;
      -webkit-mask-position-y: center;
    }
    &_b{
      background-position-y: bottom;
      // mask-position-y: bottom;
      -webkit-mask-position-y: bottom;
    }
  }

  &_v{
    &_l{
      background-position-x: left;
      // mask-position-x: left;
      -webkit-mask-position-x: left;
    }
    &_c{
      background-position-x: center;
      // mask-position-x: center;
      -webkit-mask-position-x: center;
    }
    &_r{
      background-position-x: right;
      // mask-position-x: right;
      -webkit-mask-position-x: right;
    }
  }
}

</style>
