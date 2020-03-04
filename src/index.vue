<template>
  <div class="component">
    <iframe
      v-if="url"
      :src="url"
      webkitallowfullscreen="true"
      mozallowfullscreen="true"
      allowfullscreen="true"
      frameborder="0"
      width="100%"
      marginwidth="0"
      marginheight="0"
    ></iframe>
    <div v-else>请填写iframe地址</div>
  </div>
</template>

<script>
  import {VueExtend} from 'godspen-lib'

  export default {
    mixins: [VueExtend.mixin],
    name: 'iframe',
    label: process.env.LABEL,
    style: process.env.STYLE,
    props: {
      url: {
        type: String,
        editer: {
          label: 'iframe链接'
        },
        default: ''
      }
    },
    computed: {
    },
    editorMethods: {
    },
    methods: {
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" type="text/stylus" scoped>
  .component {
    height: 100%;
    width: 100%;

    iframe {
      height: 100%;
      width: 100%;
    }
  }
</style>
