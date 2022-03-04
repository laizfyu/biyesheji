<template>
  <view>
    {{result}}
  </view>
</template>

<script>
  export default {
    
    data() {
      return {
        result: ""
      }
    },
    onLoad: function(option) {
        var that = this 
        const txt = JSON.parse(decodeURIComponent(option.txt))+"111";
        console.log("详情页:"+ txt)
        console.log("过来了")
        that.result = txt
        // return txt
    },
    methods: {
      
    }
  }
</script>

<style lang="scss">

</style>
