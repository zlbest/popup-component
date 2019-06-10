<template>
    <div class="wrapper" v-if="show">
        <div class="mask" v-show="position!='top'" @touchstart.prevent="closeModal"></div>
        <main :class="{[mainClass]: true}">
            <slot></slot>
        </main>
    </div>
</template>

<script>
    export default {
        name: "popup",
        inheritAttrs: false,
        props: {
            /* popup弹出位置 */
            position: {
                type: String,
                required: true,
            },
            /* popup显示控制 */
            show: {
                type: Boolean,
                default: false, 
            }
        },
        computed: {
            /* 内容窗口样式类名 */
            mainClass: function() {
                return `main-${this.position}`
            }
        },
        watch: {
            /* 顶部toast显示 */
            show(val) {
                if(val && this.position=='top') {
                    setTimeout(() => {
                        this.$emit("update:show", false);
                    }, 2500)
                }
            }
        },
        methods: {
            //关闭弹窗
            closeModal() {
                this.$emit("update:show", false);
            }
        }
            
    }
</script>

<style lang="scss" scoped>
    @import "../../style/mixin";
    .wrapper {
        position: fixed;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
    }
    main {
        position: absolute;
        background: #fff;
        z-index: 2;
    }
    .mask {
        position: absolute;
        top: 0;
        left: 0;
        @include wh(100vw, 100vh);
        background: rgba(0,0,0,0.6);
        z-index: 1;
    }
    .main-top {
        top: 0;
        left: 0;
        @include wh(100vw, 80px);
        line-height: 80px;
        padding-left: 15px;
        background: rgba(0,0,0,0.8);
        @include sc(30px, #fff);
        @include text-line();
        animation: slide-top .3s ease-out alternate;
    }
    .main-bottom {
        bottom: 0;
        left: 0;
        @include wh(100vw, auto);
        animation: slide-bottom .3s ease-out alternate;
    }
    .main-left {
        top: 0;
        left: 0;
        height: 100vh;
        animation: slide-left .3s ease-out alternate;
    }
    @keyframes slide-top {
        from {
            transform: translateY(-100%);
        }
        to {
            transform: translateY(0);
        }
    }
    @keyframes slide-bottom {
        from {
            transform: translateY(100%);
        }
        to {
            transform: translateY(0);
        }
    }
    @keyframes slide-left {
        from {
            transform: translateX(-100%);
        }
        to {
            transform: translateX(0);
        }
    }

</style>
