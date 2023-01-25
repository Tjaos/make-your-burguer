<template>
  <Banner/>
  <div class="main-container">
    <h1>Monte o seu burguer:</h1>
    <BurguerForm/>
  </div>
</template>

<script>
import Banner from "../components/banner.vue"
import BurguerForm from "../components/BurguerForm.vue"
export default{
  name: "Home",
  components:{
    Banner,
    BurguerForm,
  }
}
</script>
