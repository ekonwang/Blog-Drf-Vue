<template>

    <div id="header">
        <div class = "bg">
            <img :src="imgSrc" height="" width="2000">
        </div>
        <div class="grid">
            <div></div>
            <router-link :to="{ name: 'Home'}">
            <h1>Yifou 博客</h1>
            </router-link>
            <!--引入搜索框组件-->
            <SearchButton/>
        </div>
        <hr>
        <div class="login">
            <div v-if="hasLogin">
                <div class="dropdown">
                    <button class="dropbtn">欢迎, {{username}}!</button>
                    <div class="dropdown-content">
                        <router-link :to="{ name: 'UserCenter', params: { username: username }}">用户中心</router-link>
                        <router-link to="/" v-on:click.prevent="logout()">登出</router-link>
                        <router-link :to="{ name: 'ArticleCreate' }">发表文章</router-link>
                    </div>
                </div>
            </div>
            <div v-else>
                <router-link to="/login" class="login-link">登录</router-link>
            </div>
        </div>
    </div>


</template>

<script>
    import SearchButton from '@/components/SearchButton.vue';
    import authorization from '@/utils/authorization';

    export default {
        components: { SearchButton },
        name: 'BlogHeader',
        data: function () {
            return {
                //searchText: '',
                username: '',
                hasLogin: false,
                /* current: (new Date()).getTime(),
                expiredTime: Number(storage.getItem('expiredTime.myblog')),
                access: storage.getItem('access.myblog'), */
                imgSrc:require('../assets/bg-light.png')
            }
        },

        methods:{
            logout(){
                localStorage.clear();
                window.location.reload(false);
            },
            refresh() {
                this.username = localStorage.getItem('username.myblog');
            },
        },
        
        mounted() {
            authorization().then((data) => [this.hasLogin, this.username] = data); 
        }
    }
</script>

<style scoped>
    .dropbtn {
        background-color: mediumslateblue;
        color: white;
        padding: 8px 8px 30px 8px ;
        font-size: 16px;
        border: none;
        cursor: pointer;
        height: 16px;
        border-radius: 5px;
    }
    .dropdown {
        position: relative;
        display: inline-block;
    }
    .dropdown-content {
        display: none;
        position: absolute;
        background-color: #f9f9f9;
        min-width: 120px;
        box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
        text-align: center;
    }
    /* 下拉菜单的链接 */
    .dropdown-content a {
        color: black;
        padding: 12px 16px;
        text-decoration: none;
        display: block;
    }
    /* 鼠标移上去后修改下拉菜单链接颜色 */
    .dropdown-content a:hover {
        background-color: #f1f1f1
    }
    /* 在鼠标移上去后显示下拉菜单 */
    .dropdown:hover .dropdown-content {
        display: block;
    }
    /* 当下拉内容显示后修改下拉按钮的背景颜色 */
    .dropdown:hover .dropbtn {
        background-color: darkslateblue;
    }
</style>

<style scoped>
    .login-link {
        color: black;
    }

    .login {
        text-align: right;
        padding-right: 5px;
    }

    .header {
        text-align: center;
        margin-top: 10px;
        height: 100%;
        width: 100%;
        background-attachment: fixed;
    }

    .grid {
        display: grid;
        grid-template-columns: 4fr 4fr 1fr;
    }

    .bg {
        z-index : -1;
        position : absolute; 
    }


</style>