<template>
    <div class="dynamiccontent_container">
        <div class="dynamiccontent_content_container">
            <div class="dynamiccontent_content">
                <ul class="dynamic_list">
                    <li
                        class="dynamic_item"
                        v-for="(item, index) in dynamicPageList"
                        :key="index"
                    >
                        <div class="item_left">
                            <div class="item_day">
                                <div class="item_date">{{ item.date }}</div>
                                <div class="item_year">{{ item.year }}</div>
                            </div>
                            <div class="item_title_container">
                                <a
                                    v-if="!item.route && item.link"
                                    :href="item.link"
                                    target="_blank"
                                    rel="noopener noreferrer"
                                    class="item_title"
                                >
                                    {{ item.title }}
                                </a>
                                <router-link
                                    v-if="item.route"
                                    :to="item.route"
                                    class="item_title"
                                >
                                    {{ item.title }}
                                </router-link>
                                <span
                                    class="item_title_tag"
                                    v-show="currentPage === 1 && index === 0"
                                    >New</span
                                >
                            </div>
                            <div class="item_desc">{{ item.description }}</div>
                        </div>
                        <div class="item_right">
                            <a
                                v-if="!item.route && item.link"
                                :href="item.link"
                                target="_blank"
                                rel="noopener noreferrer"
                                class="item_img"
                            >
                                <img :src="item.imgName" alt="" />
                                <img v-if="!item.imgName" src="../../assets/no_article_img.png" alt="" />
                            </a>
                            <router-link
                                v-if="item.route"
                                :to="item.route"
                                class="item_img"
                            >
                                <img :src="item.imgName" alt="" />
                                <img v-if="!item.imgName" src="../../assets/no_article_img.png" alt="" />
                            </router-link>
                        </div>
                    </li>
                </ul>
                <div class="dynamic_pagination">
                    <el-pagination
                        background
                        layout="prev, pager, next"
                        :page-size="6"
                        @current-change="handlePageClick"
                        :current-page="currentPage"
                        :total="total"
                        prev-text="上一页"
                        next-text="下一页"
                    >
                    </el-pagination>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "DynamicContent",
    props: ["dynamicList"],
    data() {
        return {
            currentPage: 1,
            total: 0,
            pageSize: 6,
        };
    },
    computed: {
        dynamicPageList() {
            if (this.dynamicList.length > 0) {
                let dynamics = JSON.parse(JSON.stringify(this.dynamicList));
                return dynamics.splice((this.currentPage - 1) * 6, 6);
            }
        },
    },
    methods: {
        setTotal() {
            this.total = this.dynamicList.length;
        },
        handlePageClick(page) {
            this.currentPage = page;
        },
    },
    mounted() {
        this.setTotal();
    },
};
</script>

<style lang="stylus">
.dynamiccontent_container {
    width: 100%;
    background: #F5F6FB;

    .dynamiccontent_content_container {
        box-sizing: border-box;
        margin: 0 auto;
        padding: 6.4rem 0 8rem;
        max-width: $contentWidth;

        .dynamiccontent_content {
            margin: 0 auto;
            max-width: 100.8rem;
            @media (max-width: 1104px) {
                box-sizing: border-box;
                padding-left: 4.8rem;
                padding-right: 4.8rem;
            }
            @media (max-width: 400px) {
                padding-left: 1.6rem;
                padding-right: 1.6rem;
            }

            .dynamic_list {
                box-sizing: border-box;
                padding: 3.2rem 3.2rem 3.1rem;
                width: 100%;
                background: #fff;
                border-radius: 0.4rem;
                @media (max-width: 400px) {
                    padding: 1.6rem;
                }

                .dynamic_item {
                    box-sizing: border-box;
                    display: flex;
                    justify-content: space-between;
                    align-items: center;
                    padding: 2.4rem 0 2.3rem;
                    height: 100%;
                    border-bottom: 0.1rem solid #E1E5F4;
                    @media (max-width: 1104px) {
                        justify-content: center;
                    }

                    &:first-child {
                        padding-top: 0;
                    }

                    .item_left {
                        .item_day {
                            display: flex;
                            align-items: center;
                            box-sizing: border-box;
                            width: 11.2rem;
                            height: 2.4rem;
                            background: #fff;
                            border: 0.05rem solid $highlightDetailColor;
                            border-radius: 0.4rem;

                            .item_date {
                                display: flex;
                                justify-content: center;
                                align-items: center;
                                width: 6.6rem;
                                height: 100%;
                                font-size: $fontSize12;
                                font-weight: $fontWeight600;
                                line-height: 1.4rem;
                                color: #fff;
                                background: $highlightDetailColor;
                                border-radius: 0.2rem;
                            }

                            .item_year {
                                margin-left: 0.8rem;
                                font-size: $fontSize12;
                                font-weight: $fontWeight600;
                                color: rgba(0, 0, 0, 0.75);
                                line-height: 1.4rem;
                                text-align: center;
                            }
                        }

                        .item_title_container {
                            display: flex;
                            align-items: center;
                            margin-top: 1.2rem;
                            max-width: 66.4rem;

                            &:hover {
                                color: $highlightDetailColor;
                                cursor: pointer;
                            }

                            .item_title {
                                display: inline-block;
                                max-width: 66.4rem;
                                font-size: $fontSize16;
                                font-weight: $fontWeight600;
                                color: #000;
                                line-height: 2.4rem;
                                overflow: hidden;
                                white-space: nowrap;
                                text-overflow: ellipsis;
                                @media (max-width: 1104px) {
                                    white-space: normal;
                                }

                                &:hover {
                                    color: $highlightDetailColor;
                                }
                            }

                            .item_title_tag {
                                display: inline-block;
                                margin-left: 0.8rem;
                                width: 4rem;
                                height: 1.6rem;
                                background: rgba(9, 103, 233, 0.1);
                                border-radius: 0.2rem;
                                font-size: $fontSize12;
                                font-weight: $fontWeight400;
                                color: $highlightDetailColor;
                                line-height: 1.6rem;
                                text-align: center;
                            }
                        }

                        .item_desc {
                            margin-top: 1.2rem;
                            max-width: 66.4rem;
                            font-size: $fontSize14;
                            font-weight: $fontWeight400;
                            color: rgba(0, 0, 0, 0.75);
                            line-height: 2.4rem;
                            overflow: hidden;
                            text-overflow: ellipsis;
                            display: -webkit-box;
                            -webkit-box-orient: vertical;
                            -webkit-line-clamp: 3;
                        }
                    }

                    .item_right {
                        margin-left: 3.2rem;
                        width: 25rem;
                        font-size: 0;
                        @media (max-width: 1104px) {
                            display: none;
                        }

                        .item_img {
                            width: 100%;
                            height: 100%;

                            img {
                                width: 100%;
                            }
                        }
                    }
                }
            }

            .dynamic_pagination {
                margin-top: 2.4rem;
                height: 2.4rem;
                text-align: right;
                @media (max-width: 400px) {
                    text-align: center;
                }

                .el-pagination {
                    height: 100%;
                    font-weight: $fontWeight500;
                    color: rgba(0, 0, 0, 0.35);

                    .btn-prev {
                        box-sizing: border-box;
                        padding: 0 0.8rem;
                        border: 0.1rem solid #E1E5F4;

                        &:hover {
                            color: $highlightDetailColor;
                            border: 0.1rem solid $highlightDetailColor;
                        }
                    }

                    .el-pager {
                        .number {
                            border: 0.1rem solid #E1E5F4;
                        }
                    }

                    .btn-next {
                        box-sizing: border-box;
                        padding: 0 0.8rem;
                        border: 0.1rem solid #E1E5F4;

                        &:hover {
                            color: $highlightDetailColor;
                            border: 0.1rem solid $highlightDetailColor;
                        }
                    }
                }
                .el-pagination.is-background .el-pager li:not(.disabled).active {
                    background-color: $nprogressColor;
                    color: #fff!important;
                }
                .el-pagination.is-background .el-pager li:not(.disabled):hover {
                    color: $nprogressColor;
                }
            }
        }
    }
}
</style>