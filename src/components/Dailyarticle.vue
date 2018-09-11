<template>
     <div class="daily-article">
        <div class="daily-articel-title">{{news_data.title}}</div>
        <div class="daily-article-content" v-html="news_data.body"></div>
    </div>
</template>

<script>
export default{
    props:['id_data'],
    data(){
        return {
            news_data:''
        }
    },
    methods:{
        getatricle(){
        let url=this.HOST+ '/api/4/news/'+this.id_data;
         this.$http.get(url)
        .then(res=>{
            this.news_data=res.data;
        },res=>{
              console.info('调用失败');
        })
        }
    },
    watch:{
        id_data(val){
            if(val)
                this.getatricle();
        }
    }
}
</script>

<style>
.daily-article-title{
    font-size: 28px;
    font-weight: bold;
    color: #222;
    padding: 10px 0;
}

</style>
