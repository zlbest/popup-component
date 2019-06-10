<template>
    <div class=container>
        <button class="btn circular" @click="showPop(1)">顶部弹出</button>
        <button class="btn" @click="showPop(2)">底部弹出</button>
        <button class="btn ellipse" @click="showPop(3)">左侧弹出</button>
        <!-- popup顶部弹窗 -->
        <popup :show.sync="showTop" position="top">
            <span>{{msg}}</span>
        </popup>
        <!-- popup底部弹窗 -->
        <popup :show.sync="showBottom" position="bottom">
            <div class="popup-bottom">
                底部弹出内容
            </div>
        </popup>
        <!-- popup左侧弹窗 -->
        <popup :show.sync="showLeft" position="left">
            <div class="popup-left">
                左侧弹出内容
            </div>
        </popup>
    </div>
</template>

<script>
    import popup from '../../components/demo/popup'
    export default {
        data() {
            return {
                showTop: false,
                showBottom: false,
                showLeft: false,
                msg: '有新消息通知了~~',

            }
        },
        components: { popup },
        methods: {
           showPop(type) {
               switch(type) {
                    case 1:
                        this.showTop = true;
                        break;
                    case 2:
                        this.showBottom = true;
                        break;
                    case 3:
                        this.showLeft = true;
                        break;
                   default:
               }
           }
        }
    }
</script>

<style lang="scss" scoped>
    @import "../../style/mixin";
    .container {
        width: 100vw;
        min-height: 100vh;
        overflow-y: auto;
        -webkit-overflow-scrolling: touch;
        box-sizing: border-box;
    }
    .btn {
        display: block;
        @include wh(150px, 150px);
        line-height: 150px;
        margin: 160px auto;
        text-align: center;
        @include sc(30px, #fff);
        background: $primary;
        border: none;
        outline: none;
        box-shadow: 0 0 0 0 rgba($primary,0.5);
        transition: all 200ms;
        animation: pulse 3s infinite;
        &.circular {
            border-radius: 50%;
        }
        &.ellipse {
            border-radius: 50% / 100% 100% 0 0;
        }
    }
    
    @keyframes pulse {
        50% {
            box-shadow: 0 0 0 60px rgba($primary, 0);
        }
        100% {
            box-shadow: 0 0 0 0 rgba($primary, 0);
        }
    }

    .popup-bottom {
        @include wh(100vw, 500px);
        padding-top: 200px;
        @include sc(32px, black);
        text-align: center;
    }
    .popup-left {
        width: 400px;
        margin-top: 500px;
        @include sc(32px, black);
        text-align: center;
    }
</style>
