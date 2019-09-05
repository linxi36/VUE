<template>
  <div class="phone-body">
    <!-- {{posts}} -->
    <div class="feed" v-if="step === 1" v-dragscroll>
      <vuegramPost v-for="(post,index) in posts" :key="index" :post="post"></vuegramPost>
    </div>
    <div v-if="step ===2">
      <div 
       class="select-image"
       :class="selectFilter" 
       :style="{backgroundImage : 'url('+image+')'}"></div>
      <div class="filter-container" v-dragscroll>
        <FilterType 
        v-for="filter in filters" 
        :key="filter.name" 
        :filter="filter" 
        :image="image"></FilterType>
      </div>
    </div>
    <div v-if="step ===3">
      <div 
       class="select-image"
       :class="selectFilter" 
       :style="{backgroundImage : 'url('+image+')'}">
       </div>
       <div class="caption-container">
           <textarea 
           placeholder="Write a caption...."
           :value="value"
           @input="inputText"
           ></textarea>
       </div>
    </div>
  </div>
</template>
<script>
import vuegramPost from "./vuegramPost";
import { filter } from "minimatch";
import FilterType from "./filterType";
export default {
  //接受父组件传的值 值的类型为数组
  props: {
    posts: Array,
    step: Number,
    image: String,
    filters: Array,
    selectFilter: String,
    value : String
  },
  components: {
    vuegramPost,
    FilterType
  },
  methods:{
      inputText(event){
          this.$emit('input',event.target.value);
      }
  }
};
</script>


<style src="../style/post.css">
</style>




