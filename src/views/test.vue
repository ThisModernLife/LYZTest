<template>
    <div class="test">

        <div class="table-box" v-for="(item,index) in serveData"
             :key="index">

            <p :class="index !== 0 ? getResult[index][0].val === item.name ? 'active' : '' : ''">
                {{item.name}}
            </p>

            <p :class="index !== 0 ? getResult[index][1].val === item.age ? 'active' : '' : ''">
                {{item.age}}
            </p>

            <p :class="index !== 0 ? getResult[index][2].val === item.from ? 'active' : '' : ''">
                {{item.from}}
            </p>

            <p :class="index !== 0 ? getResult[index][3].val === item.worktime ? 'active' : '' : ''">
                {{item.worktime}}
            </p>

        </div>

    </div>
</template>

<script>
    export default {
        name: "test",
        data() {
            return {
                /**
                 * 后台数据
                 * */
                serveData: [
                    {'name': 'jack', 'age': '20', 'from': 'cn', 'worktime': 'am', 'index': '1'},
                    {'name': 'jack', 'age': '21', 'from': 'ad', 'worktime': 'am', 'index': '2'},
                    {'name': 'jack', 'age': '21', 'from': 'ua', 'worktime': 'am', 'index': '3'},
                    {'name': 'jack', 'age': '23', 'from': 'cn', 'worktime': 'pm', 'index': '4'},
                    {'name': 'jack', 'age': '24', 'from': 'us', 'worktime': 'am', 'index': '5'},
                    {'name': 'jack', 'age': '24', 'from': 'us', 'worktime': 'am', 'index': '6'},
                    {'name': 'rose', 'age': '30', 'from': 'cn', 'worktime': 'pm', 'index': '7'},
                    {'name': 'jack', 'age': '10', 'from': 'ad', 'worktime': 'am', 'index': '8'}
                ]
            }
        },
        mounted() {
            let that = this;
            console.log(that.getResult)
        },
        methods: {
            /**
             * 排除第一个的，所有内容
             * 其实是所有需要对比的数据 第二条到最后一条
             * */
            getR() {
                let that = this;
                let r = {};
                for (let i = 0; i < that.serveData.length; i++) {
                    if (i === 0) {
                    } else {
                        r[i - 1] = Array.from(Object.values(that.serveData[i]));
                    }
                }
                return r;
            },
            /**
             * 排除最后一个的，所有内容
             * 其实所有需要对比数据的参照数据 第一条到倒数第二条
             * */
            getL() {
                let that = this;
                let l = {};
                for (let i = 0; i < that.serveData.length; i++) {
                    if (i === that.serveData.length - 1) {
                    } else {
                        l[i] = Array.from(Object.values(that.serveData[i]));
                    }
                }
                return l;
            },
            /**
             * 获取所有的对比结果
             * */
            result() {
                let that = this;
                let c = {};
                for (let k in that.getR()) {
                    let b = [];
                    for (let j in that.getR()[k]) {
                        let a = {};
                        if (that.getL()[k][j] !== that.getR()[k][j]) {
                            a['val'] = that.getR()[k][j]

                        }
                        b.push(a)
                    }
                    c[parseInt(k) + 1] = b;
                }
                return c;
            }
        },
        computed: {
            getResult() {
                let that = this;
                return that.result()
            }
        }
    }
</script>

<style lang="scss">
    .test {
        .table-box {
            p {
                display: inline-block;
                width: calc(100% / 4);
                line-height: 4;
                text-align: center;
                border-bottom: 1px solid black;
                font-size: 30px;
            }
        }

        .active {
            background-color: #2d8cf0;
            color: #fff;
        }
    }
</style>
