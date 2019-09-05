<template>
  <div class="vuegram-post">
    <div class="header level">
      <div class="level-left">
        <figure class="image is-32x32">
          <img :src="post.userImage" alt />
        </figure>
        <span class="username">{{post.username}}</span>
      </div>
    </div>
    <div
      class="img-container"
      :style="{backgroundImage:'url('+post.postImage+')'}"
      :class="post.filter"
      :dblclick="clicklike"
    ></div>
    <div class="footer">
      <div class="hreat">
        <i
        @click="clicklike"
        :class="classname"></i>
      </div>
      <p class="likes">{{post.likes}} likes</p>
      <p class="caption">
        <span>{{post.username}}</span>
        {{post.caption}}
      </p>
    </div>
  </div>
</template>
<script>
export default {
    props : {
        post : Object,
    },
    data(){
      return {
        classname : 'iconfont icon-aixin1',
      }
    },
    methods : {
      clicklike (){
      this.post.hasBeenLiked ? this.post.likes-- : this.post.likes++;
      this.post.hasBeenLiked = !this.post.hasBeenLiked ;
      if(this.classname == 'iconfont icon-aixin1'){
            this.classname = 'iconfont icon-aixin'
      }else if(this.classname == 'iconfont icon-aixin'){
        this.classname = 'iconfont icon-aixin1'
      }
     }
    }
};
</script>
<style src="../style/post.css">
</style>


