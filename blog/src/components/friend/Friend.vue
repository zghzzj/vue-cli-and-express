<template>
    <div   class="blog-home">
        <div class="blog-child">

         <div v-for="(item,index) in friendList" :key="index" class="friend-item" @click="See(item.link)">
            <el-row type="flex" class="row-bg" justify="space-between">
                <el-col :span="4"><div class="grid-content bg-purple">{{item.name}}</div></el-col>
                 <el-col :span="15"><div  class="link">{{item.link}}</div></el-col>
            </el-row>
            <el-row type="flex" class="introduce" v-if="item.introduce!=''?true:false">
                <el-col :span="12"><div class="grid-content bg-purple" >博客介绍：{{item.introduce}}</div></el-col>         
            </el-row>
         </div>
        </div>
    </div>
</template>

<script>
export default {
    created() {
        this.getFriendList();
    },
    name:'Friend',
    data(){
        return {
            friendList:[]
        }
    },
    components:{
        
        
    },
    mounted(){
      
    },
    methods: {
        async getFriendList(){
            let res = await this.$axios.get('/friend_list',{params:{
                offset:0,
                limit:30
            }})
          
            if(res.status === 200){
                if(res.data.code === 0){
                let data = res.data.data
                console.log(data)
                this.friendList = data.list
 
                }

            }

        },
        See (e) {
           window.open(e);
        }

    },
}
</script>

<style >
   a:link { text-decoration: none;}  
   .introduce{
       color:#9c9797;
       margin-top: 10px;
       text-align:justify;
       text-justify:distribute-all-lines;
   }
   .friend-item{
       width:95%;
       border:1px solid #f5f1f1;
       margin: auto;
       box-shadow: 2px 2px 15px #eee;
       margin-top: 20px;
       box-sizing: border-box;
       padding:20px;
   }
   .link{
       text-align: right;
   }
</style>