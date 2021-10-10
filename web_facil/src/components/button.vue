<template>
  <div class="button">
    <button type="submit" class="btn btn-primary mt-4">{{msg}}</button>
  </div>
</template>

<script>
export default {
  name: 'button',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.btn{
    width: 310px;
    border-radius: 15px;
    background: #483698;
    font-family: 'Open Sans', sans-serif;
}
@media screen and (width: 360px) {
  .btn{
    width: 290px;
  }
}
</style>
