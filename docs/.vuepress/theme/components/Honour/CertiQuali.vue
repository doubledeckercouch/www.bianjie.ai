<template>
    <div class="certiquali_container">
        <div class="certiquali_content_container">
            <div class="certiquali_content">
                <div class="title">{{ certiQualiContent.title }}</div>
                <div class="sub_title">{{ certiQualiContent.subTitle }}</div>
                <ul class="list">
                    <li
                        class="item"
                        v-for="(item, index) in certiQualiContent.list"
                        :key="index"
                    >
                        <div class="item_img">
                            <!-- data-action -->
                            <img :src="differentImg(item.src)" alt="" />
                        </div>
                        <div class="item_right">
                            <div class="right_title">{{ item.title }}</div>
                            <div class="item_desc">{{ item.description }}</div>
                        </div>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "CertiQuali",
    props: ["certiQualiContent"],
    computed: {
        differentImg() {
            return function(imgName) {
                return `/about/zizhi/${imgName}`;
            }
        }
    }
};
</script>

<style lang="stylus">
.certiquali_container {
    width: 100%;
    background: #fff;

    .certiquali_content_container {
        box-sizing: border-box;
        padding: 6.4rem 0 4.8rem;
        margin: 0 auto;
        max-width: $contentWidth;
        height: 100%;

        .certiquali_content {
            margin: 0 auto;
            max-width: 100.8rem;
            height: 100%;
            @media (max-width: 768px) {
                box-sizing: border-box;
                padding-left: 4.8rem;
                padding-right: 4.8rem;
            }
            @media (max-width: 375px) {
                padding-left: 1.6rem;
                padding-right: 1.6rem;
            }

            .title {
                font-size: $fontSize24;
                font-weight: $fontWeight500;
                color: #000;
                line-height: 2.4rem;
                text-align: center;
            }

            .sub_title {
                margin-top: 1.6rem;
                font-size: $fontSize14;
                font-weight: $fontWeight400;
                color: rgba(0, 0, 0, 0.75);
                line-height: 2rem;
                text-align: center;
            }

            .list {
                margin: 4rem auto 0;
                display: grid;
                grid-template-columns: repeat(2, 1fr);
                grid-row-gap: 2.4rem;
                grid-column-gap: 4.8rem;
                @media (max-width: 1050px) {
                    grid-template-columns: repeat(1, 1fr);
                    max-width: 48rem;
                }

                .item {
                    display: flex;
                    justify-content: space-between;
                    align-items: center;
                    box-sizing: border-box;
                    padding: 1.6rem;
                    max-width: 48rem;
                    min-height: 22.4rem;
                    border: 0.1rem solid #E1E5F4;
                    border-radius: 0.4rem;
                    @media (max-width: 574px) {
                        flex-direction: column;
                        justify-content: center;
                    }

                    .item_img {
                        display: flex;
                        justify-content: center;
                        align-items: center;
                        margin-right: 1.6rem;
                        max-width: 15.8rem;
                        height: 19.2rem;
                        @media (max-width: 574px) {
                            margin-right: 0;
                        }

                        img {
                            height: 100%;
                        }
                    }

                    .item_right {
                        max-width: 27.4rem;
                        @media (max-width: 574px) {
                            margin-top: 1.6rem;
                        }

                        .right_title {
                            font-size: $fontSize16;
                            font-weight: $fontWeight600;
                            color: #000;
                            line-height: 2.4rem;
                            @media (max-width: 574px) {
                                text-align: center;
                            }
                        }

                        .item_desc {
                            margin-top: 0.3rem;
                            font-size: $fontSize14;
                            font-weight: $fontWeight400;
                            color: rgba(0, 0, 0, 0.75);
                            line-height: 2.4rem;
                        }
                    }
                }
            }
        }
    }
}
</style>