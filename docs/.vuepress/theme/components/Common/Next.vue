<template>
    <div class="next_container">
        <div class="next_content">
            <span class="next"><i class="iconfont icon-jiantou"></i></span>
        </div>
    </div>
</template>

<script>
export default {
    name: "Next",
};
</script>

<style lang="stylus">
.next_container {
    box-sizing: border-box;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 4.8rem;
    height: 4.8rem;
    background: rgba(255, 255, 255, 0.5);
    border-radius: 50%;
    outline: none;

    &:hover {
        cursor: pointer;
    }

    .next_content {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 4rem;
        height: 4rem;
        border: 0.2rem solid $highlightDetailColor;
        border-radius: 50%;

        .next {
            font-weight: $fontWeight500;
            color: $highlightDetailColor;
        }
    }
}
</style>