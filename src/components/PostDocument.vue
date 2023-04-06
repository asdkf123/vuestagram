<template>
  <div class="post" >
    <div class="post-header">
<!--      <img :src="post.userImage" class="profile" alt="">-->
      <div class="profile" :style="{ backgroundImage :`url(${post.userImage}`}"></div>
      <span class="profile-name">{{post.name}}</span>
    </div>
<!--    <img :src="post.postImage" class="post-body">-->
    <div class="post-body"
         :style="{ backgroundImage :`url(${post.postImage}`}"></div>
    <div class="post-content">
      <p>{{ post.likes }}</p>
      <p><strong>{{ post.content }}</strong></p>
      <p class="date">{{ post.date }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "PostDocument",
  props: {
    post: Object,
  },
}
</script>

<style scoped>
.post {
  width: 100%;
}
.profile {
  /*background-image: url("https://placeimg.com/100/100/arch");*/
  width: 30px;
  height: 30px;
  background-size: 100%;
  border-radius: 50%;
  float: left;
}
.profile-name {
  display: block;
  float: left;
  padding-left: 10px;
  padding-top: 7px;
  font-size: 14px;
}
.post-header {
  height: 30px;
  padding: 10px;
}
.post-body {
  /*background-image: url("https://placeimg.com/640/480/animals");*/
  height: 450px;
  width: 100%;
  /*height: 100%;*/
  background-position: center;
  background-size: cover;
}
.post-content {
  padding-left: 15px;
  padding-right: 15px;
  font-size: 14px;
}
.date {
  font-size: 11px;
  color: grey;
  margin-top: -8px;
}
</style>