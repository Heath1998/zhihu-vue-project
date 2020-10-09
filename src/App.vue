<template>
  <div id="app">
    <div class="daily-menu">
      <div class="daily-menu-item" :class="{'on':type==='recommend'}" @click="handlerecommend()"> 
        <p>每日推荐</p>
      </div>
      <div class="daily-menu-item" :class="{'on':type==='daily'}" @click="handledaily()"> 
        <p>主题日报</p>
      </div>
    </div>
    <div class="daily-list">
      <div v-for="list in itemlist"  :key="list.id" @click="handleToArticle(list.id)">
      <Item  :aloneitem="list" :type="type"> </Item>
      </div>
    </div>
    <div class="articleclass">
      <Dailyarticle :id_data="id"></Dailyarticle>
    </div>
  </div>
</template>

<script>
import Item from './components/Item.vue';
import Dailyarticle from './components/Dailyarticle'; 
export default {
  data(){
    return {
      type:'recommend',
      itemlist:'',
      recommendlist:'',
      dailylist:'',
      id:'',
    }
  },
  components:{
    Item,
    Dailyarticle
  },
  methods:{
    handlerecommend(){
      this.type='recommend';
    },
    handledaily(){
      this.type='daily';
    },
     handleToArticle(i){
      this.id=i;
      console.log(this.id);
    }
  },
  watch:{
    type(newval){
      if(newval==='daily')
      {
        this.itemlist=this.dailylist;
      }
      else if(newval){
       this.itemlist=this.recommendlist;
      }
    }
  },
  mounted(){
    var url = '/api/4/news/latest'
    this.$http.get(url)
    .then(res => {
      console.log(res.data);
      this.itemlist=res.data.stories;
      this.recommendlist=res.data.stories;
      this.dailylist=res.data.top_stories;
      console.log(res.data.stories);
      console.log(res.data.stories[9].images[0]);
  
    },res => {
      console.info('调用失败');
    });
      }
    }
</script>

<style>
html,body{
  margin: 0;
  padding: 0;
  height: 100%;
  color: #657180;
  font-size: 16px;
}
.daily-menu{
  width: 10%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  overflow: auto;
  background: #f5f7f9;
}
.daily-menu-item{
  padding: 5% 0;
  
}
.on{
    border-right: 2px solid #3399ff;
}
.daily-menu-item p{
  text-align: center;
  color:#3399ff;
   cursor: pointer;
  
}
.daily-list{
  width: 20%;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 10%;
  overflow: auto;
  border-right: 1px solid #d7dde4;
}
.articleclass{
  position: fixed;
  top: 0;
  bottom: 0;
  width:67%;
  margin-left: 30%;
  padding: 20px;
  overflow: auto;

}
</style>
