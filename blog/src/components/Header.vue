<template>
    <div class="site-header">
        <div class="site-header-wrap">
            <div class="site-header-inside">
                <div class="site-branding">
                    <p class="profile">
                        <router-link to="/index">
                            <img src="../assets/logo.png" alt="">
                           <!-- <div class="img" style="margin:0 auto;width:100px;height:100px;background:url('https://blog.zenggenghai.cn/public/static/img/logo.ff0996c.png') center center repeat-x"></div>   -->
                        </router-link>
                    </p>
                    <div class="site-identify">
                        <h1>曾耿海</h1>
                        <p>WEB DEVELOPER</p>
                    </div>
                    <div class="site-nav-inside">
                        <ul class="menu">
                            <li class="menu-item" v-for="(item,index) in list" :key="item.title">
                                <router-link :class="{'menu-item-select':itemCheck==index}" :to="item.path"  @click.native="tabClass(index)">{{item.title}}</router-link>
                            </li>
                           
                        </ul>
                    
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:'Header',
    data(){
        return {
            list:[
                {
                    title:'文章列表',
                    path:"/index"
                },{
                    title:'文档收纳',
                     path:"/note"
                },{
                    title:'随笔记录',
                     path:"/lifeRecord"
                },{
                    title:'友情链接',
                     path:"/friend"
                }
            ],
            itemCheck:0
            
        }
    },
    components:{

    },
    methods:{
        tabClass(index){
            this.itemCheck = index;
        },
        fetchData(){
           console.log('路由发送变化doing...');
        }
    },
    created(){ 
        // if(this.$route.name === "article"){
        //     this.itemCheck = 2;
        // }else if( this.$route.name === "about"){
        //     this.itemCheck = 1
        // }else{
        //     this.itemCheck = 0;
        // }
      
        this.list.forEach((element,index) => {
        
                let reg = '^[^/]*\/';
                let res = this.$route.name.replace(reg,''); 
                console.log(res) 
                // console.log(element.title)
                // if(element.title == res){  
                //     this.itemCheck = index;
                // } 
                if(res == "article"){
                    this.itemCheck = 0;
                }
                if(res == "note" || res == "article"){
                    this.itemCheck = 1;
                }
                if(res == "lifeRecord" ){
                    this.itemCheck = 2;
                }
                if(res == "friend" ){
                    this.itemCheck = 3;
                }
             
        });
        
     
    },
    watch:{
     
    },




}
</script>

<style scoped>
    body{
        font-size: 10px;
      
    }
    a{
        text-decoration:none;
    }
    .site-header{
        background:#000;
        color:#fff;
        height:100%;
        position:fixed;
        left:0;
        top:0;
        text-align: center;
        z-index: 9999;
        /* box-shadow:0 2px 12px 0 rgba(0,0,0,.4) */
    }
    .profile img{
        width:90px;
        border:2px solid #d4a259;
        border-radius:50%;
    }
    .site-identify{
        padding-bottom:1.6em;
    }
    .site-identify h1{
        font-size:22px;
        line-height: 1;
    }
    .site-identify p{
        font-size:12px;
        color:rgba(102,102,102);
    }
    .menu{
        font-size:0.8rem;
        color:#aaa;
        line-height: 1.5;
        letter-spacing:0.15em;
        text-transform:uppercase;
       
        padding:0;
    }
    .menu-item{
        list-style:none;
      

    }
    .menu-item{
      
        padding:0.5rem 0;
    }
    .menu-item a{
        color:#aaa;
        cursor:pointer;
    }
    .menu-item a:hover{
        color:#d4a259
    }
    .menu-item-select{
        color:#d4a259 !important;
    }



    @media only screen and (min-width:1001px){
        .site-header{
            width:300px;
        }
        .site-header-inside{
            padding-left:30px;
            padding-right:30px;
            padding-bottom:3.333em;
            padding-top:5.333em
        }
           /* .site-header-wrap{
            display: flex;
            flex-direction: column;
            justify-content: center;
        } */
    }
    @media only screen and (min-width:801px) and (max-width:1001px){
        .site-header{
            width:30vw;
        }
        .site-header-inside{
            padding-bottom:3.3333em;
            padding-top:5.3333em;
            height:400px;
        }
     
        
    }
    @media only screen and (max-width:800px){
        .site-header{
            width:100%;
            height:78px;
            overflow-y: hidden;
   
        }
 
        .profile img{
            width:50px;
        }
    }

    .site-header-wrap{
        height:100%;
        /* overflow:auto;
        -webkit-overflow-scrolling:touch; */
 
    }



</style>