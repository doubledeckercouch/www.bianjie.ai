<template>
    <div class="iritaopb_title_container">
        <div class="iritaopb_title_content_container">
            <div class="iritaopb_title_content">
                <div class="title">{{ iritaopbTitleContent.title }}</div>
                <div class="sub_title">{{ iritaopbTitleContent.subTitle }}</div>
                <MoreBlue class="more_btn" :text="iritaopbTitleContent.moreText" @click.native="goComming"></MoreBlue>
            </div>
        </div>
    </div>
</template>

<script>
import MoreBlue from "@theme/components/Common/MoreBlue.vue";
export default {
    name: "IritaOpbTitle",
    props: ["iritaopbTitleContent"],
    methods: {
        goComming(){
            this.$router.push(`${this.$store.state.currentLang}products/IRITAOPB-敬请期待`);
        }
    },
    components: {
        MoreBlue,
    }
};
</script>

<style lang="stylus">
.iritaopb_title_container {
    width: 100%;
    height: 36rem;
    background: url('../../assets/product/iritaopb/iritaopb_banner.png') no-repeat center / cover;
    @media (max-width: 768px) {
        background: url(../../assets/product/iritahub/iritahub_banner_pad.png) no-repeat center / cover;
    }
    @media (max-width: 420px) {
        height: 25rem;
        background: url(/banner_phone.png) no-repeat center / cover;
    }

    .iritaopb_title_content_container {
        margin: 0 auto;
        max-width: $contentWidth;
        height: 100%;

        .iritaopb_title_content {
            display: flex;
            flex-direction: column;
            justify-content: center;
            box-sizing: border-box;
            margin: 0 auto;
            max-width: 109.6rem;
            height: 100%;
            @media (max-width: 1200px) {
                padding-left: 4.8rem;
                padding-right: 4.8rem;
            }
            @media (max-width: 420px) {
                align-items: center;
                padding-left: 1.6rem;
                padding-right: 1.6rem;
            }

            .title {
                font-size: $fontSize40;
                font-weight: $fontWeight500;
                color: #000;
                line-height: 4.8rem;
                @media (max-width: 775px) {
                    font-size: $fontSize36;
                }
                @media (max-width: 420px) {
                    font-size: $fontSize22;
                    text-align: center;
                }
            }

            .sub_title {
                margin-top: 2.4rem;
                font-size: $fontSize20;
                font-weight: $fontWeight400;
                color: rgba(0, 0, 0, 0.75);
                line-height: 2.4rem;
                @media (max-width: 420px) {
                    font-size: $fontSize16;
                    text-align: center;
                }
            }

            .more_btn {
                margin-top: 4rem;
            }
        }
    }
}
</style>