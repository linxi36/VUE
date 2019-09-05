<template>
   <div class="app">
     <div class="app-phone">
       <div class="phone-header">
         <a 
         class="cancle-cta"
         v-if="step===2 || step ===3"
         @click="goToHome">Cancle</a>
         <img class="logo" src="./assets/logo.png" alt="">
         <a 
         class="next-cta"
         v-if="step===2"
         @click="step++">Next</a>
         <a 
         class="next-cta"
         v-if="step===3"
         @click="share"
         >Share</a>
       </div>
       <phoneBody 
       :posts="posts" 
       :step="step"
       :image="image"
       :filters="filters"
       :selectFilter = "selectFilter"
       v-model="caption"
       ></phoneBody>
       <div class="phone-footer">
         <div 
         class="home-cta"
         @click="goToHome">
           <i class="iconfont icon-weibiaoti-"></i>
         </div>
         <div class="upload-cta">
           <input type="file" id="file" @change="uploadIamge" :disabled='step !==1'>
           <label for="file">
            <i class="iconfont icon-add_circle" ></i>
           </label>
         </div>
       </div>
     </div>
   </div>
</template>

<script>
import phoneBody from './components/phoneBody'
import posts from './data/posts'
import filters from './data/filters'
import eventBus from './eventBus'
export default {
  name : 'app',
  created(){
      eventBus.$on('selectFilter', evt=>{
          this.selectFilter = evt;
      })
  },
  data(){
     return {
       posts,
       step : 1,
       image : '',
       filters,
       selectFilter : '',
       caption : '123'
     }
  },
  components : {
    phoneBody 
  },
  methods :{
    uploadIamge(evt){
        const files = evt.target.files;
        if(!files.length) return;
        const reader = new FileReader();
        //读取文件
        reader.readAsDataURL(files[0]);
        reader.onload = evt =>{
          this.image = evt.target.result;
          this.step = 2;
        }
    },
    goToHome(){
      this.image = '';
      this.selectFilter = '';
      this.step = 1;
    },
    share(){
      const post ={
        username : 'ice',
        userImage : 'http://s3-us-west-2.amazonaws.com/s.cdpn.io/1211695/me_3.jpg',
        postImage :this.image,
        likes:0,
        hasBeenLiked : false,
        caption : this.caption,
        filter : this.selectFilter,
      }
      //将post数据插到post.js数据最前面
      this.posts.unshift(post);
      //回到第一步
      this.goToHome();
    }
  }
}
</script>
<style src='./style/style.css'>

</style>

