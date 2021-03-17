<template>
  <div>
    <h1 id="storeName"> Ivy's Restaurant </h1>
    <PageContent> </PageContent>
  </div>
</template>

<script>
import PageContent from './components/PageContent.vue'

export default {
  components : {
    PageContent
  }
}
</script>

<style>
  #storeName {
    background-color : lightblue;
    text-align : center;
  }
</style>
