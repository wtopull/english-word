<template>
    <div id="wrapper">
        <main>
            <div class="inps flex_items">
                <!-- <div class="input-field">
                    <input value="a,b,c,d,e,f,g,h,i,j,k,l" id="first_name2" type="text" class="validate">
                </div> -->
                <div class="englishs">
                    <ul class="flex">
                        <li v-for="(item,index) in arrs" :key="index">{{item}}</li>
                    </ul>
                </div>
                <div class="inps_btn flex_items j_sb">
                    <a class="waves-effect waves-light btn" @click="autoHandle"><i class="material-icons left">autorenew</i>随机</a>
                    <a class="waves-effect waves-light btn" @click="copyHandle"><i class="material-icons left">content_copy</i>复制</a>
                    <a class="waves-effect waves-light btn" @click="searchHandle"><i class="material-icons left">search</i>查找</a>
                </div>
            </div>
            <div class="s_box">
                <h6>结果：2000个单词，12个为一组，有序组合共{{n}}组</h6>
                <h6>结果：2000个单词，12个为一组，无序组合共{{n1}}组</h6>
                <ul>
                    <li class="s_item  flex_items j_sb" v-for="(item, index) in pls" :key="index">
                        <span>{{item}}</span>
                        <a class="waves-effect waves-light btn" @click="copyHandle"><i class="material-icons left">content_copy</i>复制</a>
                    </li>
                </ul>
            </div>
        </main>
    </div>
</template>

<script>
import _ from "lodash";
import arrs from "../assets/js/index.js";
import arrsAll from "../assets/js/arrs.js";
export default {
    name: "landing-page",
    data() {
        return {
            n: 1,
            n1: 1,
            arrs: [],
            pls: [
                "A",
                "B",
                "C",
                "D",
                "E",
                "F",
                "G",
                "H",
                "I",
                "J",
                "K",
                "L",
                "A",
                "B",
                "C",
                "D",
                "E",
                "F",
                "G",
                "H",
                "I",
                "J",
                "K",
                "L",
            ],
        };
    },
    mounted() {
        this.arrs = arrs["a2"];
        this.perm(["01", "02", "03", "04"]);
        this.initNum(2000, 12);
    },
    methods: {
        // 随机
        autoHandle() {
            // let arr = _.chunk(arrsAll["arrs"], 2);
            // 1
            // let allArr = this.perm(...arr);
            // console.log(allArr);

            // 2
            // this.perm2();
            // 3
            // this.perm3();
            // 4
            this.perm4();
        },
        // 复制
        copyHandle() {},
        // 查找
        searchHandle() {},
        //排列组合1
        perm() {
            return Array.prototype.reduce.call(
                arguments,
                function (a, b) {
                    let ret = [];
                    a.forEach(function (a) {
                        b.forEach(function (b) {
                            ret.push(a.concat([b]));
                        });
                    });
                    return ret;
                },
                [[]]
            );
        },
        // 排列组合2
        perm2() {
            let arr = [
                [
                    "a0",
                    "a1",
                    "a2",
                    "a3",
                    "a4",
                    "a5",
                    "a6",
                    "a7",
                    "a8",
                    "a9",
                    "a10",
                    "a11",
                ],
                [
                    "a12",
                    "a13",
                    "a14",
                    "a15",
                    "a16",
                    "a17",
                    "a18",
                    "a19",
                    "a20",
                    "a21",
                    "a22",
                    "a23",
                ],
            ];
            let results = [];
            let result = [];
            doExchange(arr, 0);
            function doExchange(arr, index) {
                for (let i = 0; i < arr[index].length; i++) {
                    result[index] = arr[index][i];
                    if (index != arr.length - 1) {
                        doExchange(arr, index + 1);
                    } else {
                        results.push(result.join(","));
                    }
                }
            }
            console.log(results);
            console.log(_.chunk(results, 12));
        },
        // 排列组合3
        perm3() {},
        // 排列组合4
        perm4() {
            let arr = arrsAll["arrs"].slice(0, 10);
            function cmn(m, n, currentIndex = 0, choseArr = [], result = []) {
                let mLen = m.length;
                if (currentIndex + n > mLen) {
                    return;
                }
                for (let i = currentIndex; i < mLen; i++) {
                    if (n === 1) {
                        result.push([...choseArr, m[i]]);
                        i + 1 < mLen && cmn(m, n, i + 1, choseArr, result);
                        break;
                    }
                    cmn(m, n - 1, i + 1, [...choseArr, m[i]], result);
                }
                return result;
            }
            console.log("结果：：", cmn(arr, 2));
        },
        // 计算组数
        initNum(s, z) {
            this.n = sub(s + 1, s + 1 - z);
            this.n1 = Math.ceil(sub(s + 1, s + 1 - z) / sub(z + 1, 1));
            function sub(m, n) {
                let h = 1;
                for (let i = n; i < m; i++) {
                    h *= i;
                }
                return h;
            }
        },
    },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Source+Sans+Pro");
@import url("~@/assets/css/index.css");
</style>
