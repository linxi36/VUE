<template>
    <div class="filter-type">
        <p>{{filter.name}}</p>
        <div 
        class="img"
        :class="filter.name"
        :style="{backgroundImage : 'url('+image+')'}"
        @click="selectFilter"
        ></div>
    </div>
</template>
<script>
import eventBus from '../eventBus'
export default {
    props :{
        filter : Object,
        image : String,
    },
    methods : {
        selectFilter(){
            eventBus.$emit('selectFilter',this.filter.name);
        }
    }
}
</script>

<style src="../style/filter.css">

</style>


