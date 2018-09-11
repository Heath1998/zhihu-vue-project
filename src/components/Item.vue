<template>
    <div class="daily-item">
        <div class="daily-img" v-if="type==='recommend'">
            <img :src="aloneitem.images[0]" alt="加载失败">
        </div>
        <div class="daily-img" v-else>
            <img :src="aloneitem.image" alt="加载失败">
        </div>
         <div class="daily-title" >{{aloneitem.title}}</div>
    </div>
</template>

<script>
export default {
    props:['aloneitem','type'],

    data(){
        return{

        }
    },
    methods:{ 

    },
}
</script>

<style>
.daily-item{
    display: block;
    color: inherit;
    text-decoration: none;
    padding: 16px;
    overflow: hidden;
    cursor: pointer;
    transition: all 0.3s ease-in-out;
}
.daily-img{
    float: left;
    height: 80px;
    width: 80px;
   
}

.daily-img img{
    width: 100%;
    height: 100%;
    border-radius: 3px;
}
.daily-title{
    padding: 10px 5px 10px 90px;
}
</style>
