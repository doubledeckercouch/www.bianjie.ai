<template>
    <div class="plan_adv_container">
        <div class="plan_adv_content_container">
            <div class="plan_adv_content">
                <div class="plans_title">{{plansContent.plansTitle}}</div>
                <ul class="plans_intro">
                    <li class="plans_intro_item" v-for="(item,index) in plansContent.plansIntro" :key="index">{{item.intro}}</li>
                </ul>
                <div class="product_title">{{plansContent.productTitle}}</div>
                <ul class="advantage_list">
                    <li class="advantage_item" v-for="(adv,index) in plansContent.advantageList" :key="index">
                        <div class="advantage_img">
                            <img :src="differentIcon(adv.iconName)" alt="" />
                        </div>
                        <div class="advantage_right">
                            <div class="adv_text">{{adv.advantageText}}</div>
                            <div class="adv_desc">{{adv.description}}</div>
                        </div>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'PlanAdvantage',
    props: ['plansContent'],
    computed: {
        differentIcon() {
            return function (imgName) {
                return `/appscenes/icon/${imgName}`;
            };
        },
    }
}
</script>

<style lang="stylus">
.plan_adv_container {
    width: 100%;
    min-height: 86rem;
    background: #FCFCFC;
    .plan_adv_content_container {
        box-sizing: border-box;
        padding: 4.8rem 0 6rem;
        margin: 0 auto;
        max-width: $contentWidth;
        .plan_adv_content {
            margin: 0 auto;
            max-width: 90rem;
            @media (max-width: 996px) {
                box-sizing: border-box;
                padding-left: 4.8rem;
                padding-right: 4.8rem;
            }
            @media (max-width: 375px) {
                padding-left: 1.6rem;
                padding-right: 1.6rem;
            }
            .plans_title {
                font-size: $fontSize24;
                font-weight: $fontWeight500;
                color: #000;
                line-height: 2.4rem;
                text-align: center;
            }
            .plans_intro {
                margin-top: 4rem;
                font-size: $fontSize14;
                font-weight: $fontWeight400;
                color: rgba(0, 0, 0, 0.75);
                line-height: 2.4rem;
                .plans_intro_item {
                    margin-top: 2.4rem;
                    &:first-child {
                        margin-top: 0;
                    }
                }
            }
            .product_title {
                margin-top: 4.8rem;
                font-size: $fontSize24;
                font-weight: $fontWeight500;
                color: #000;
                line-height: 2.4rem;
                text-align: center;
            }
            .advantage_list {
                margin-top: 4rem;
                .advantage_item {
                    display: flex;
                    align-items: center;
                    box-sizing: border-box;
                    margin: 2.4rem auto 0;
                    padding: 2.8rem 2.4rem;
                    max-width: 73.6rem;
                    min-height: 12rem;
                    background: #fff;
                    border: 0.1rem solid #E1E5F4;
                    border-radius: 0.4rem;
                    @media (max-width: 400px) {
                        flex-direction: column;
                    }
                    &:first-child {
                        margin-top: 0;
                    }
                    .advantage_img {
                        display: flex;
                        justify-content: center;
                        align-items: center;
                        margin-right: 2.4rem;
                        width: 6.4rem;
                        height: 6.4rem;
                        @media (max-width: 400px) {
                            margin-right: 0;
                        }
                        img {
                            height: 100%;
                        }
                    }
                    .advantage_right {
                        @media (max-width: 400px) {
                            margin-top: 1.6rem;
                        }
                        .adv_text {
                            font-size: $fontSize16;
                            font-weight: $fontWeight600;
                            color: #000;
                            line-height: 1.6rem;
                            @media (max-width: 400px) {
                                text-align: center;
                            }
                        }
                        .adv_desc {
                            margin-top: 0.8rem;
                            font-size: $fontSize14;
                            font-weight: $fontWeight400;
                            color: rgba(0, 0, 0, 0.75);
                            line-height: 2.4rem;
                            @media (max-width: 400px) {
                                text-align: center;
                            }
                        }
                    }
                }
            }
        }
    }
}
</style>