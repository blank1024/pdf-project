<!--
 * @Description:
 * @Date: 2020-03-06 21:41:59
 * @Author: jawnwa22
 * @LastEditors: jawnwa22
 * @LastEditTime: 2020-03-09 17:24:47
 -->
<template>
    <div class="pdf-container">
        <div class="pdf-header">
            <div class="pdf-title">订单合同</div>
            <div class="company-logo">
                <img src="@/assets/images/logo.png" alt />
            </div>
        </div>
        <div class="info">
            <div class="info-row">
                <div class="left">电话：</div>
                <div class="right">传真：</div>
            </div>
            <div class="info-row">
                <div class="left">电邮：it@sdfsdf.cn</div>
                <div class="right">官网：123123</div>
            </div>
            <div class="info-row">
                <div class="left">地址：123123</div>
            </div>
        </div>
        <table class="table-container">
            <tbody>
                <tr>
                    <td width="15%">订单号</td>
                    <td colspan="3">123123121231231213</td>
                </tr>
                <tr>
                    <td>To(公司)</td>
                    <td>老油条</td>
                    <td width="15%">From(公司)</td>
                    <td>平头哥</td>
                </tr>
                <tr>
                    <td>交货日期</td>
                    <td></td>
                    <td>日期</td>
                    <td>2020-01-01</td>
                </tr>
            </tbody>
        </table>
        <product-list></product-list>
        <table class="table-container">
            <tbody>
                <tr>
                    <td>运费：</td>
                    <td>金额</td>
                    <td>¥1232423</td>
                </tr>
                <tr>
                    <td>
                        <div>开票资料</div>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import productList from './productList.vue';
export default {
    components: {
        productList
    },
    data() {
        return {};
    },
    mounted() {
        this.transformPDF();
    },
    methods: {
        transformPDF() {
            let html = document.documentElement;
            let s = html.innerHTML;
            s = s.replace(/"/g, "'");
            this.$axios.$post('/dc/convert/html/pdf',{
                s
            }).then( res => {
                console.log(res.pdf_url);
            })
        }
    }
    // asyncData({ $axios }) {
    //     return $axios
    //         .$get("/mallapi/som/order/contract/info", {
    //             params: {
    //                 order_id: "000000007057953e0170622af08e0028"
    //             },
    //             headers: {
    //                 SOM_ACCESS_TOKEN: "8e478311035446da81c52009a8bdaa41",
    //                 SOM_UID: "92973224-f47e-431a-baae-487817cecd33",
    //                 SOM_PLATFORM: "SLMS"
    //             }
    //         })
    //         .then(res => {
    //             return { info: res };
    //         });
    // }
};
</script>

<style lang="less" scoped>
.vc {
    display: flex;
    align-items: center;
}

.pdf-container {
    width: 210mm;
    margin: 0 auto;
    padding: 20px;
    position: relative;
}

.pdf-header {
    margin-bottom: 10px;
    height: 22px;
    position: relative;
    .pdf-title {
        text-align: center;
    }
    .company-logo {
        position: absolute;
        left: 0;
        top: 0;
        width: 150px;
        height: 100%;
        .vc();
        img {
            max-width: 100%;
            max-height: 100%;
        }
    }
}

.info {
    font-size: 12px;
    .info-row {
        display: flex;
        line-height: 20px;
        .left {
            flex: 2;
        }
        .right {
            flex: 1;
        }
    }
}
</style>
