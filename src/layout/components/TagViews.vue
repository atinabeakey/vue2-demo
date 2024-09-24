<template>
    <div class="tag-views">
        <ul>
            <li v-for="(item, index) in visitedViews" :key="index" :class="{ active: activeIndex === index }">

                <p>
                    {{ item.title }}sss
                </p>
                <i class="el-icon-close hidden"></i>
            </li>
        </ul>
    </div>
</template>
<script>
export default {
    data() {
        return {
            visitedViews: [
                { title: 1, },
                { title: 2, },
                { title: 3, },
            ],
            activeIndex: 1
        }
    }
}
</script>
<style lang="scss" scoped>
.tag-views {
    position: absolute;
    top: 50px;
    left: 0;
    z-index: 3;
    height: 40px;
    line-height: 40px;
    width: 100%;
    box-shadow: 0 1px 4px rgba(0, 21, 41, 0.08);

    ul {
        display: flex;
        padding-left: 20px;

        li {
            margin-right: 20px;
            cursor: pointer;
            display: flex;
            align-items: center;

            p {
                position: relative;

                &::after {
                    content: '';
                    display: inline-block;
                    width: 100%;
                    height: 2px;
                    background: transparent;
                    position: absolute;
                    bottom: 0;
                    left: 0;
                }
            }


            &.active {
                color: #1ddcc9;

                p {
                    &::after {
                        background: #1ddcc9;
                    }
                }

            }

            .hidden {
                margin-left: 5px;
                visibility: hidden;
            }

            &:hover {
                .hidden {
                    visibility: visible;
                }
            }

        }
    }
}
</style>