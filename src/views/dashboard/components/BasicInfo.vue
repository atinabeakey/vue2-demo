<template>
    <div class="basic-info">
        <div class="title">
            <div>
                <p>光伏逆变器</p>
                <p>回路：1#塑壳/1#微端</p>
            </div>
            <p class="normal"><i class="el-icon-circle-check"></i>&nbsp;正常</p>
        </div>
        <div class="img">
            <img src="@/assets/img/guangfu.png" alt="" />

        </div>
        <div class="info">
            <p>
                <span>
                    <i class="el-icon-s-flag"></i>
                    总发电量(KW-h)
                </span>
                <b>15803</b>
            </p>
            <p>
                <span>
                    <i class="el-icon-coordinate"></i>
                    总有功功率(KW)
                </span>
                <b>15803</b>
            </p>
            <p>
                <span>
                    <i class="el-icon-suitcase-1"></i>
                    今日发电(KW-h)
                </span>
                <b>15803</b>
            </p>

        </div>
        <div class="basic">
            <div class="basic-title">
                <i class="el-icon-document"></i>
                基本信息
            </div>
            <p>
                <label>设备名称</label>
                <b>阳光电源逆变器</b>
            </p>
            <p>
                <label>型号</label>
                <b>SG-X</b>
            </p>
            <p>
                <label>SN序列号</label>
                <b>XFSFFFFFFFFFF</b>
            </p>
            <p>
                <label>额定有功功率</label>
                <b>27.87KW</b>
            </p>
        </div>
    </div>
</template>
<style lang="scss" scoped>
.basic-info {
    height: 100%;
    padding: 20px;

    .title {
        display: flex;
        justify-content: space-between;
        align-items: center;

        div {
            p {
                font-size: 12px;
                color: #c9cfd2;

                &:nth-of-type(1) {
                    font-size: 16px;
                    font-weight: 600;
                    color: #2c3e50;
                    margin-bottom: 5px;
                }
            }
        }

        .normal {
            padding: 5px 20px;
            color: #1ddcc9;
            border-radius: 20px;
            background: #e5fbf9;
        }

    }

    .img {
        width: 180px;
        margin: 10px auto;

        img {
            width: 100%;
        }
    }

    .info {
        padding-bottom: 20px;
        border-bottom: 1px solid #f2f2f2;

        p {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-bottom: 10px;

            span {
                color: #a1acb2;
                font-size: 13px;
            }
        }
    }

    .basic {
        padding-top: 30px;

        .basic-title {
            font-size: 16px;
            font-weight: 600;
            color: #2c3e50;
            padding-bottom: 20px;
        }

        p {
            display: flex;
            align-items: center;
            padding-bottom: 10px;

            label {
                color: #a1acb2;
                font-weight: normal;
                width: 110px;
            }


        }
    }
}
</style>