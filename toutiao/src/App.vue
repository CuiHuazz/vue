<template>
  <div id="app">
      <div class="tabwrap" v-show="isBottom">
          <div class="tab-item">
              <router-link to="/index">
                  <div class="icon icon1"></div>
                  <div class="icon-word">首页</div>
              </router-link>
          </div>
          <div class="tab-item">
              <router-link to="/collection">
                  <div class="icon icon2"></div>
                  <div class="icon-word">收藏</div>
              </router-link>
          </div>
          <div class="tab-item">
              <router-link to="/follow">
                  <div class="icon icon3"></div>
                  <div class="icon-word">关注</div>
              </router-link>
          </div>
          <div class="tab-item">

              <router-link to="/my">
                  <div class="icon icon4"></div>
                  <div class="icon-word">我的</div>
              </router-link>
          </div>
      </div>

        <transition :name="transitionName">
         <!--<transition name="fade">-->
            <keep-alive>
                <router-view></router-view>
            </keep-alive>
        <!--</transition>-->
        </transition>

  </div>
</template>

<script>
  import {ajax} from './common/js/ajax'
  export default {
      name: 'app',
      components:{
      },
      data(){
          return {
              transitionName:'',
              isBottom:true,
              bottomArr:['/index','/collection','/follow','/my']
          }
      },
      methods:{

      },
      watch: {
          '$route' (to, from) {
               this.transitionName = JSON.parse(window.sessionStorage.history).transitionName;
               let index = this.bottomArr.indexOf(to.path);
               if(index == -1){
                   this.isBottom = false;
               }else{
                   this.isBottom = true;
               }
          }
      },
      created(){

      },
      updated(){
//         console.log(this.$router);
      }

  }
</script>

<style rel="stylesheet/scss" lang="scss">
    @import "./common/scss/index";
    #app {
        height: 100%;
        .tabwrap {
            width: 100%;
            position: fixed;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #fff;
            display: flex;
            height: 45px;
            padding-top: 5px;
            z-index: 99;
            @include border-1px(#eee);

            .tab-item {
                flex: 1;
                text-align: center;
                .icon {
                    width: 0.48rem;
                    height: 0.48rem;
                    background-size: 100% auto;
                    background-repeat: no-repeat;
                    margin: 0 auto;
                    &.icon1 {
                        background-image: url(./assets/demo/icon11.png);
                    }
                    &.icon2 {
                        background-image: url(./assets/demo/icon21.png);
                    }
                    &.icon3 {
                        background-image: url(./assets/demo/icon31.png);
                    }
                    &.icon4 {
                        background-image: url(./assets/demo/icon41.png);
                    }
                }
                .icon-word {
                    font-size: 12px;
                    margin-top: 5px;
                }
                & .active {
                    .icon1 {
                        background-image: url(./assets/demo/icon12.png);
                    }
                    .icon2 {
                        background-image: url(./assets/demo/icon22.png);
                    }
                    .icon3 {
                        background-image: url(./assets/demo/icon32.png);
                    }
                    .icon4 {
                        background-image: url(./assets/demo/icon42.png);
                    }
                    .icon-word {
                        color: red;
                    }
                }
            }
        }

        .fade-enter-active, .fade-leave-active {
            transition: all 0.3s;
        }
        .fade-enter, .fade-leave-to {
            opacity: 0;
        }

        //微信切换样式 ，左右滚动
        //前进动画样式
        .forward-enter-active,.forward-leave-active{
            transition: all 0.3s;
        }

        .forward-enter{
            transform: translateX(100%);
        }
        .forward-leave-to{
            transform: translateX(-100%);
        }

        // 后退动画样式
        .reverse-enter-active,.reverse-leave-active{
            transition: all 0.3s;
        }
        .reverse-enter{
            transform: translateX(-100%);
        }
        .reverse-leave-to{
            transform: translateX(100%);
        }

    }





</style>
