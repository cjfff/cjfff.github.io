mode = markdown
```vue
<template>
  <div class="mode-page">
    <vue-article-view 
      v-show="!loading"
      :content="content"
      mode="markdown"
      @loading="handleLoading"
      @loaded="handleLoaded"
    />
    <div class="loading-wrap" v-show="loading">
        <div class="donut"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      content: '',
      loading: false
    }
  },
  mounted() {
    this.loading = true
    fetch('./static/demo.md').then(res => res.text())
      .then(res => {
        setTimeout(() => this.content = res, 500)
      })
  },
  methods: {
    // 内部开始执行计算
    handleLoading() {
      console.log('loading')
    },
    handleLoaded() {
      console.log('loaded')
      this.loading = false
    }
  }
}
</script>
<style lang="less">
.mode-page {
 .deepexi-document-view .deepexi-scrollbar {
    &.fixed {
      right: 50px;
      top: 50px;
    }
  }
  .loading-wrap {
    width: 936px;
    height: 500px;
    text-align: center;
    line-height: 500px;
  }
}

@keyframes donut-spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
.donut {
  display: inline-block;
  border: 4px solid rgba(0, 0, 0, 0.1);
  border-left-color: #7983ff;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  animation: donut-spin 1.2s linear infinite;
}

</style>
```