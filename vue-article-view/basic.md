基本用法
```vue
<template>
  <div class="basic-page">
      <vue-article-view :content="content" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      content: ''
    }
  },
  mounted() {
    fetch('./static/demo.html').then(res => res.text())
      .then(res => {
        this.content = res
      })
  }
}
</script>
<style lang="less">
.basic-page {
  .deepexi-document-view .deepexi-scrollbar {
    &.fixed {
      right: 50px;
      top: 50px;
    }
  }
}
</style>
```