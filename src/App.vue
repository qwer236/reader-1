<template>
    <div id="app">
        <main>
            <router-view/>
        </main>
        <footer>
            <nav>
                <router-link tag="div" :to="{name: 'Home'}" exact>
                    <i class="fa fa-home"></i>
                    <span>首页</span>
                </router-link>
                <router-link tag="div" :to="{name: 'Category'}">
                    <i class="fa fa-anchor"></i>
                    <span>分类</span>
                </router-link>
                <router-link tag="div" :to="{name: 'Cart'}">
                    <i class="fa fa-shopping-cart"></i>
                    <span>购物车</span>
                </router-link>
                <router-link tag="div" :to="{name: 'Me'}">
                    <i class="fa fa-user"></i>
                    <span>我</span>
                </router-link>
            </nav>
        </footer>
    </div>
</template>

<script>
    export default {
        name: 'App'
    }
</script>

<style lang="scss">
@import 'assets/style/normalize.css';
@import 'assets/style/app.scss'   
</style>