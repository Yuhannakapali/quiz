<template>
  <div>
    <b-nav>
      <b-nav-item disabled>Quiz app</b-nav-item>
      <b-nav-item disabled> counter : {{ correctAnswer }}/{{ totalAnswer}}</b-nav-item>
     
    </b-nav>
  </div>
</template>
<script>
export default {
  props:
    [
    'correctAnswer',
    'totalAnswer'
    ]
    
  
}
</script>
<style  scoped>

</style>
