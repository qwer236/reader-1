<template>
    <div>
        <header>首页</header>
        <div class="content">
            <!-- 轮播图 -->
            <div class="swiper-container">
                <div class="swiper-wrapper">
                    <div class="swiper-slide">
                        <img src="../../assets/img/1.jpg">
                    </div>
                    <div class="swiper-slide">
                        <img src="../../assets/img/2.jpg">
                    </div>
                    <div class="swiper-slide">
                        <img src="../../assets/img/3.jpg">
                    </div>
                </div>
                <div class="swiper-pagination"></div>
                <div class="swiper-button-next"></div>
                <div class="swiper-button-prev"></div>
            </div>
            <!-- 广告部分 -->
            <div class="ad-box">
                <i class="fa fa-bell"></i>
                <p>
                    双12全场图书5折优惠，更有神秘惊喜大奖等你来！
                </p>
            </div>
            <!-- 书籍加载部分 -->

            <div class="books-box clearfix" :title-message="tit1">
                <h3>{{tit1}}</h3>
                <div class="book-list" v-for="book in newBooks" :key="book.id">
                    <img :src="book.cover">
                    <p>{{book.name}}</p>
                    <p class="color-txt">
                        <span>￥</span> {{book.price}}</p>
                </div>
            </div>

            <div class="books-box clearfix" :title-message="tit1">
                <h3>{{tit2}}</h3>
                <div class="book-list" v-for="book in recomend" :key="book.id">
                    <img :src="book.cover">
                    <p>{{book.name}}</p>
                    <p class="color-txt">
                        <span>￥</span> {{book.price}}</p>
                </div>
            </div>

            <div class="books-box clearfix" :title-message="tit1">
                <h3>{{tit3}}</h3>
                <div class="book-list" v-for="book in hotBooks" :key="book.id">
                    <img :src="book.cover">
                    <p>{{book.name}}</p>
                    <p class="color-txt">
                        <span>￥</span> {{book.price}}</p>
                </div>
            </div>

        </div>

    </div>
</template>

<script>
    import "swiper/dist/css/swiper.css";
    import Swiper from "swiper";
    export default {
        name: "",
        data() {
            return {
                tit1: "新书上架",
                tit2: "编辑推荐",
                tit3: "热门新书",
                newBooks: [],
                recomend: [],
                hotBooks: []
            };
        },
        methods: {
            // 轮播图函数
            runSwiper() {
                var swiper = new Swiper(".swiper-container", {
                    spaceBetween: 30,
                    centeredSlides: true,
                    autoplay: {
                        delay: 2500,
                        disableOnInteraction: false
                    },
                    pagination: {
                        el: ".swiper-pagination",
                        clickable: true
                    },
                    navigation: {
                        nextEl: ".swiper-button-next",
                        prevEl: ".swiper-button-prev"
                    }
                });
            },
            //书籍请求函数
            creatBooks() {
                axios.all([
                    axios.get("../../../static/api/new-book.json"),
                    axios.get("../../../static/api/recommend.json"),
                    axios.get("../../../static/api/hot-newbook.json")
                ]).then(axios.spread((perms1, perms2, perms3) => {
                    this.newBooks = perms1.data
                    this.recomend = perms2.data
                    this.hotBooks = perms3.data
                }));
            }
        },
        mounted() {
            this.runSwiper();
        },
        created() {
            this.creatBooks()
        }
    };

</script>

<style lang="scss" scoped>
    @import "./home.scss";

</style>
