<template>
    <div class="search">
        <form>
            <input v-model="searchText" type="text" placeholder="输入搜索内容...">
            <button v-on:click.prevent="searchArticles"></button>
        </form>
    </div>
</template>

<script>
    export default {
        name: 'SearchButton',
        data: function () {
            return {
                searchText: '',
            }
        },
        methods: {
            searchArticles() {
                const text = this.searchText.trim();
                if (text.charAt(0) !== '') {
                    this.$router.push({name: 'Home', query: { search: text }})
                }
            }
        },
    }
</script>

<style scoped>
    #header {
        text-align: center;
        margin-top: 20px;
    }

    .grid {
        display: grid;
        grid-template-columns: 1fr 4fr 1fr;
    }

    .search {
        padding-top: 22px;
    }

    /* css 来源：https://blog.csdn.net/qq_39198420/article/details/77973339*/
    * {
        box-sizing: border-box;
    }

    form {
        position: relative;
        width: 200px;
        margin: 0 auto;
    }

    input, button {
        border: none;
        outline: none;
    }

    input {
        width: 100%;
        height: 35px;
        padding-left: 13px;
        padding-right: 46px;
    }

    button {
        height: 35px;
        width: 35px;
        cursor: pointer;
        position: absolute;
    }

    .search input {
        border: 2px solid gray;
        border-radius: 5px;
        background: transparent;
        top: 0;
        right: 0;
    }

    .search button {
        background: gray;
        border-radius: 0 5px 5px 0;
        width: 45px;
        top: 0;
        right: 0;
    }

    .search button:before {
        content: "搜索";
        font-size: 13px;
        color: white;
    }
    .login-link {
        color: black;
    }

    .login {
        text-align: right;
        padding-right: 5px;
    }
</style>
