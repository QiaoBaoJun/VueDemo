<template lang="html">
    <div class="shopcart">
        <div class="content">
            <div class="content-left">
                <div class="logo-wrapper">
                    <div class="logo" :class="{highlight: totalCount>0}">
                        <i class="icon-shopping_cart"></i>
                    </div>
                    <div class="count" v-show="totalCount>0">{{totalCount}}</div>
                </div>
                <div class="price" :class="{highlight: totalCount>0}">
                    ￥{{totalPrice}}
                </div>
                <div class="desc">
                    另需配送费￥{{deliveryPrice}}元
                </div>
            </div>
            <div class="content-right">
                <div class="pay" :class="{enough: totalPrice >= minPrice}">
                    {{payDesc}}
                </div>
            </div>
        </div>
        <div class="ball-container">

        </div>
    </div>
</template>

<script>
export default {
    props: {
        selectFoods: {
            type: Array,
            default () {
                return [{
                    price: 13,
                    count: 0
                }]
            }
        },
        deliveryPrice: {
            type: Number,
            default: 0
        },
        minPrice: {
            type: Number,
            default: 0
        }
    },
    computed: {
        totalPrice () {
            let total = 0
            this.selectFoods.forEach((food) => {
                total += food.price * food.count
            })
            return total
        },
        totalCount () {
            let count = 0
            this.selectFoods.forEach((food) => {
                count += food.count
            })
            return count
        },
        payDesc () {
            if (this.totalPrice === 0) {
                return `￥${this.minPrice}元起送`
            } else if (this.totalPrice < this.minPrice) {
                return `还差${this.minPrice - this.totalPrice}元起送`
            } else {
                return '去结算'
            }
        }
    }
}
</script>

<style lang="scss" rel="stylesheet/scss">
    .shopcart {
        position: fixed;
        left: 0;
        bottom: 0;
        z-index: 50;
        width: 100%;
        height: 48px;
        .content {
            display: flex;
            background-color: #141d27;
            font-size: 0;
            color: rgba(255,255,255,0.4);
            .content-left {
                flex: 1;
                .logo-wrapper {
                    display: inline-block;
                    vertical-align: top;
                    position: relative;
                    top: -10px;
                    margin: 0 12px;
                    padding: 6px;
                    width: 56px;
                    height: 56px;
                    box-sizing: border-box;
                    border-radius: 50%;
                    background-color: #141d27;
                    .count {
                        position: absolute;
                        top: 0;
                        right: 0;
                        width: 24px;
                        height: 16px;
                        line-height: 16px;
                        text-align: center;
                        border-radius: 16px;
                        font-size: 9px;
                        font-weight: 700;
                        color: #fff;
                        background-color: rgb(240,20,20);
                        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.4);
                    }
                    .logo {
                        width: 100%;
                        height: 100%;
                        border-radius: 50%;
                        background-color: #2b343c;
                        text-align: center;
                        &.highlight {
                            background-color: rgb(0,160,220);
                            .icon-shopping_cart {
                                color: #fff;
                            }
                        }
                        .icon-shopping_cart {
                            color: #80858a;
                            font-size: 24px;
                            line-height: 44px;
                        }
                    }
                }
                .price {
                    display: inline-block;
                    vertical-align: top;
                    margin-top: 12px;
                    line-height: 24px;
                    padding-right:12px;
                    box-sizing: border-box;
                    border-right: 1px solid rgba(255,255,255,0.1);
                    font-size: 16px;
                    font-weight: 700;
                    &.highlight {
                        color: #fff;
                    }
                }
                .desc {
                    display: inline-block;
                    vertical-align: top;
                    margin: 12px 0 0 12px;
                    line-height: 24px;
                    font-size: 10px;
                    font-weight: 400;
                }
            }
            .content-right {
                flex: 0 0 105px;
                width: 105px;
                background-color: #2b333b;
                .pay {
                    height: 48px;
                    line-height: 48px;
                    text-align: center;
                    font-size: 12px;
                    font-weight: 700;
                    &.enough {
                        background-color: #00b43c;
                        color: #fff;
                    }
                }
            }
        }
    }
</style>
