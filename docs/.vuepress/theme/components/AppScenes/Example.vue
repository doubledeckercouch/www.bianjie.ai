<template>
    <div class="example_container">
        <div class="example_content_container">
            <div class="example_content">
                <div class="example_title">{{exampleContent.title}}</div>
                <div class="example">
                    <div class="example_img">
                        <img :src="exampleContent.example.imgName" alt="" />
                    </div>
                    <div class="example_right">
                        <div class="example_text">{{exampleContent.example.text}}</div>
                        <div class="example_desc">{{exampleContent.example.intro}}</div>
                        <a class="example_link" v-if="!exampleContent.example.route && exampleContent.example.link" :href="exampleContent.example.link" target="_blank" rel="noopener noreferrer">
                            <More class="more_btn" :text="exampleContent.moreText"></More>
                        </a>
                        <router-link class="example_link" v-if="exampleContent.example.route" :to="exampleContent.example.route">
                            <More class="more_btn" :text="exampleContent.moreText"></More>
                        </router-link>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import More from '@theme/components/Common/More';
export default {
    name: 'Example',
    props: ['exampleContent'],
    components: {
        More
    }
}
</script>

<style lang="stylus">
.example_container {
    width: 100%;
    min-height: 44.8rem;
    .example_content_container {
        box-sizing: border-box;
        margin: 0 auto;
        padding: 6rem 0 12rem;
        max-width: $contentWidth;
        .example_content {
            margin: 0 auto;
            max-width: 100rem;
            min-height: 31.2rem;
            @media (max-width: 1030px) {
                box-sizing: border-box;
                padding-left: 4.8rem;
                padding-right: 4.8rem;
            }
            @media (max-width: 552px) {
                padding-left: 1.6rem;
                padding-right: 1.6rem;
            }
            .example_title {
                font-size: $fontSize24;
                font-weight: $fontWeight500;
                color: #000;
                line-height: 2.4rem;
                text-align: center;
            }
            .example {
                box-sizing: border-box;
                display: flex;
                align-items: center;
                margin-top: 4rem;
                height: 100%;
                border: 0.05rem solid #E1E5F4;
                @media (max-width: 1030px) {
                    flex-direction: column;
                    padding: 4.8rem;
                }
                @media (max-width: 1030px) {
                    flex-direction: column;
                    padding: 4.8rem;
                }
                @media (max-width: 400px) {
                    padding: 0 0 1.6rem;
                }
                .example_img {
                    display: flex;
                    align-items: center;
                    width: 36rem;
                    height: 100%;
                    font-size: 0;
                    @media (max-width: 1030px) {
                        margin-right: 0;
                    }
                    @media (max-width: 400px) {
                        width: 100%;
                    }
                    img {
                        width: 100%;
                    }
                }
                .example_right {
                    display: flex;
                    flex-direction: column;
                    box-sizing: border-box;
                    padding-left: 6rem;
                    padding-right: 6rem;
                    max-width: 64rem;
                    @media (max-width: 1030px) {
                        align-items: center;
                        margin-top: 3.2rem;
                        padding-left: 0rem;
                        padding-right: 0rem;
                    }
                    @media (max-width: 400px) {
                        box-sizing: border-box;
                        padding: 0 1.6rem;
                    }
                    .example_text {
                        font-size: $fontSize16;
                        font-weight: $fontWeight600;
                        color: #000;
                        line-height: 2.4rem;
                        overflow: hidden;
                        white-space: nowrap;
                        text-overflow: ellipsis;
                        @media (max-width: 1030px) {
                            white-space: normal;
                        }
                    }
                    .example_desc {
                        margin-top: 1.6rem;
                        font-size: $fontSize14;
                        font-weight: $fontWeight400;
                        color: rgba(0,0,0,0.74);
                        line-height: 2.4rem;
                    }
                    .example_link {
                        display: inline-block;
                        margin-top: 2.4rem;
                        .more_btn {
                            border: 0.1rem solid $highlightDetailColor;
                            border-radius: 0.2rem;
                        }
                    }
                }
            }
        }
    }
}
</style>