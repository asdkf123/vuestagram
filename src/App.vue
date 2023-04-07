<template>
  <div class="header">
    <ul class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right" >
      <li v-if="step === 1" @click="step++;">Next</li>
      <li v-if="step === 2" @click="publish">발행</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>

  <PostContainer :instagramData="instagramData"
                 :step="step"
                 :uploadedImage="uploadedImage"
                 @wroteMessage="changeContent"
  />

  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="uploadFile" type="file" id="file" class="inputfile" />
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>
  <button @click="loadMorePost">더보기</button>
</template>

<script>

import PostContainer from "@/components/PostContainer.vue";
import instagramData from "@/assets/postData";
import axios from "axios";

export default {
  name: 'App',
  components: {
    PostContainer,
  },
  data() {
    return {
      instagramData,
      step: 0,
      clickCount: 0,
      uploadedImage:'',
      wroteMessage: '',
    };
  },
  methods: {
    loadMorePost() {
      axios.get(`https://codingapple1.github.io/vue/more${this.clickCount}.json`).then((res) => {
        this.instagramData = this.instagramData.concat(res.data);
        this.clickCount++;
      });
    },
    uploadFile(e) {
        let file = e.target.files;
        console.log(file);
        let url = URL.createObjectURL(file[0]);
        console.log(url);
        this.step++;
        this.uploadedImage = url;
    },
    publish() {
      let newPost = {
        name: "lodi",
        userImage: "https://placeimg.com/100/100/arch",
        postImage: this.uploadedImage,
        likes: 0,
        date: "May 15",
        liked: false,
        content: this.wroteMessage,
        filter: "perpetua"
      }
      this.instagramData.unshift(newPost);
      this.step = 0;
    },
    changeContent(content) {
      this.wroteMessage = content;
    }
  }
}
</script>

<style>
body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
</style>
