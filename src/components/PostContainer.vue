<template>
  <div>
    <PostDocument v-for="(value, i) in instagramData" :key="i"
    :post="instagramData[i]"
    />
  </div>
</template>

<script>
import PostDocument from "@/components/PostDocument.vue";
import instagramData from "@/assets/postData";
export default {
  name: "PostContainer",
  components: {PostDocument},
  data () {
    return {
      instagramData,
    }
  }
}
</script>

<style scoped>

</style>