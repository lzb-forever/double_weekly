<template>
  <div>
    <div v-if="show" class="loading">
      <div class="loadbox">
        <img src="../../assets/img/medicne/loading.gif" /> 数据分析中...
      </div>
    </div>
    <test class="canvas" style="opacity: .2; width: 100%; height: 100%"></test>
    <div class="showlood" v-if="!show">
      <!--header-->
      <div class="head">
        <h1>北京医疗美容行业月度数据报表</h1>
        <div class="weather">
          <!-- <span id="showTime">2019-09-15</span>
          <span id="showTime">至</span>
          <span id="showTime">2019-09-30</span> -->
          <span  id="showTime">{{month}}</span>
        </div>
      </div>

      <div class="mainbox">
        <ul class="clearfix">
          <li>
            <div class="boxall" style="height: 280px">
              <div class="alltitle">本月门店数量走势图</div>

              <linegraph
                class="allnav"
                :id="'bargraph1'"
                :data="shopCountOption"
                style="height: 230px; width: 97%"
              ></linegraph>
              <div class="boxfoot"></div>
            </div>
            <div class="boxall" style="height: 280px">
              <div class="alltitle">三分(效果、环境、服务)分布状况</div>
              <linegraph
                class="allnav"
                :id="'bargraph2'"
                :data="trisectionOption"
                style="height: 230px; width: 97%"
              ></linegraph>
              <div class="boxfoot"></div>
            </div>
            <div class="boxall" style="height: 280px">
              <div class="alltitle">近12个月首评分布</div>
              <linegraph
                class="allnav"
                :id="'bargraph3'"
                :data="decemberOption"
                style="height: 230px; width: 97%"
              ></linegraph>
              <div class="boxfoot"></div>
            </div>
          </li>
          <li>
            <div class="bar">
              <div class="barbox">
                <ul class="clearfix">
                  <li class="pulll_left counter">
                    {{shopOnlineCount}}
                    <br />
                    {{shopCount}}
                  </li>
                  <li class="pulll_left counter">
                    {{orderCount}}
                    <br />
                    ￥{{saleMoneyCount}}
                    <!-- ￥ 213,12.12 -->
                  </li>
                </ul>
              </div>
              <div class="barbox2">
                <ul class="clearfix">
                  <li class="pulll_left">
                    具备上线资质门店数
                    <br />当前总门店数
                  </li>
                  <li class="pulll_left">
                    本月总订单数
                    <br />本月总销售额
                  </li>
                </ul>
              </div>
            </div>
            <div class="map">
              <div class="map1">
                <img src="../../assets/img/medicne/lbx.png" />
              </div>
              <div class="map2">
                <img src="../../assets/img/medicne/jt.png" />
              </div>
              <div class="map3">
                <img src="../../assets/img/medicne/map.png" />
              </div>

              <!-- 地图 -->
              <linegraph
                class="map4"
                :id="'bargraphMap'"
                :data="mapOption"
                style="width: 650px;
                height: 650px;
                position: relative;
                left: 0.7rem;
                top: 1%;
                margin-top: 0.2rem;
                z-index: 5;"
              ></linegraph>
            </div>
          </li>
          <li>
            <div class="boxall" style="height: 280px">
              <div class="alltitle">月度好评/差评详情</div>
              <linegraph
                class="allnav"
                :id="'bargraph4'"
                :data="commentOption"
                style="height: 230px; width: 97%"
              ></linegraph>
              <div class="boxfoot"></div>
            </div>
            <div class="boxall" style="height: 280px">
              <div class="alltitle">星级门店分布</div>
              <linegraph
                class="allnav"
                :id="'bargraph5'"
                :data="startOption"
                style="height: 230px; width: 97%"
              ></linegraph>
              <div class="boxfoot"></div>
            </div>
            <div class="boxall" style="height: 280px">
              <div class="alltitle">本月医美热搜词</div>

              <wordcloud
                style="height: 230px; width: 97%"
                :rotate="{from: -30, to: 30, numOfOrientation: 5 }"
                :margin="{top: 5, right: 5, bottom: 5, left: 5 }"
                :data="ym_hot_kw"
                nameKey="name"
                valueKey="value"
                :color="myColors"
                :showTooltip="true"
                :wordClick="wordClickHandler"
              ></wordcloud>
              <div class="boxfoot"></div>
            </div>
          </li>
        </ul>
        <ul>
          <li class="w100">
            <div class="alltitle">月度行业指标详情</div>
            <table class="t_table">
              <thead>
                <tr>
                  <th colspan="2">{{month}}</th>
                  <th v-for="(item,index) in data_x" :key="index">{{item}}</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td rowspan="5" style="width: 30px;">
                    门
                    <br />店
                    <br />数
                  </td>
                  <td style="width: 100px;">总门店数</td>
                  <td v-for="(item,index) in shop_count_list" :key="index">{{item}}</td>
                </tr>
                <tr>
                  <td>有资质数</td>
                  <td v-for="(item,index) in shop_aptitude_list" :key="index">{{item}}</td>
                </tr>
                <tr>
                  <td>5星门店数</td>
                  <td v-for="(item,index) in start_5_list" :key="index">{{item}}</td>
                </tr>
                <tr>
                  <td>4.5星门店数</td>
                  <td v-for="(item,index) in start_4_5_list" :key="index">{{item}}</td>
                </tr>
                <tr>
                  <td>4星门店数</td>
                  <td v-for="(item,index) in start_4_list" :key="index">{{item}}</td>
                </tr>
                <tr>
                  <td rowspan="6">
                    评
                    <br />论
                  </td>
                  <td>总评论数</td>
                  <td v-for="(item,index) in comment_count_list" :key="index">{{item}}</td>
                </tr>
                <tr>
                  <td>5星</td>
                  <td v-for="(item,index) in comment_5_list" :key="index">{{item}}</td>
                </tr>
                <tr>
                  <td>4星</td>
                  <td v-for="(item,index) in comment_4_list" :key="index">{{item}}</td>
                </tr>
                <tr>
                  <td>3星</td>
                  <td v-for="(item,index) in comment_3_list" :key="index">{{item}}</td>
                </tr>
                <tr>
                  <td>2星</td>
                  <td v-for="(item,index) in comment_2_list" :key="index">{{item}}</td>
                </tr>
                <tr>
                  <td>1星</td>
                  <td v-for="(item,index) in comment_1_list" :key="index">{{item}}</td>
                </tr>
              </tbody>
            </table>
          </li>
          <li class="w100" style="margin-top: .5rem;">
            <div class="alltitle">本月5星评论增加量门店排名 TOP20</div>
            <table class="t_table_yc">
              <thead>
                <tr>
                  <th>排名</th>
                  <th>门店主图</th>
                  <th>门店ID</th>

                  <th>门店名称</th>
                  <th>5星评论增量</th>
                  <th>地址</th>

                  <th>电话</th>
                  <th>星级</th>
                  <th>环境分</th>

                  <th>效果分</th>
                  <th>服务分</th>
                  <th>产品数</th>

                  <th>总卖量</th>
                  <th>本月卖量</th>
                  <th>总评论数</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(item,index) in dianPingYmsTop" :key="index">
                  <td style="font-size: .4rem; font-weight: 500; font-style: italic;">{{index +1}}</td>
                  <td width="80">
                    <img style="padding: 0.1rem;" :src="item.defaultPic" />
                  </td>
                  <td>{{item.id}}</td>

                  <td>{{item.name}}</td>
                  <td>{{item.start_5_add}}</td>
                  <td>{{item.address}}</td>

                  <td>{{item.phoneNum}}</td>
                  <td>
                    <el-rate v-model="item.shopPower" :disabled="true" text-color="#ff9900"></el-rate>
                  </td>
                  <td>{{item.envScore}}</td>

                  <td>{{item.qualityScore}}</td>
                  <td>{{item.serviceScore}}</td>
                  <td>{{item.product_count}}</td>

                  <td>{{item.orderCount}}</td>
                  <td>{{item.monthOrderCount}}</td>
                  <td>{{item.reviewCount}}</td>
                </tr>
              </tbody>
            </table>
          </li>
        </ul>
      </div>
      <div class="mainbox">
        <ul class="clearfix">
          <li style="width: 100%">
            <div class="t_header_product" style="margin-top: 0.5rem">
              <span>北京医美行业产品概览</span>
            </div>
          </li>
          <li style=" width: 100%; display: flex; align-items: center; justify-content: center;">
            <div class="t_box" style="margin-right: 0.3rem">
              <header class="t_title">
                <span>品种类总卖量排名 TOP10</span>
              </header>
              <linegraph
                class="allnav"
                :id="'bargraph7'"
                :data="echart_product_type"
                style="height: 430px; width: 98%"
              ></linegraph>
            </div>
            <div class="t_box">
              <header class="t_title">
                <span>本月品种类卖量排名 TOP10</span>
              </header>
              <linegraph
                class="allnav"
                :id="'bargraph8'"
                :data="chart_product_type_add"
                style="height:430px; width: 98%"
              ></linegraph>
            </div>
          </li>

          <li
            style=" width: 100%; display: flex; align-items: center; justify-content: center; margin-top: .25rem"
          >
            <div class="t_box" style="margin-right: 0.3rem;padding-bottom: 0.4rem;">
              <header class="t_title">
                <span>种类总卖量变化曲线图 TOP5</span>
              </header>
              <linegraph
                class="allnav"
                :id="'bargraph9'"
                :data="chart_product_sales_top5"
                style="height:400px; width: 98%"
              ></linegraph>
            </div>

            <div class="t_box" style="padding-bottom: 0.4rem;">
              <header class="t_title">
                <span>种类本月卖量变化曲线图 TOP5</span>
              </header>
              <linegraph
                class="allnav"
                :id="'bargraph10'"
                :data="chart_product_add_sales_top5"
                style="height:400px; width: 98%"
              ></linegraph>
            </div>
          </li>
          <li
            style=" width: 100%; display: flex; align-items: center; justify-content: center; margin-top: .25rem"
          >
            <div class="t_box" style="margin-right: .4rem; height:auto;">
              <header class="t_title">
                <span>产品总销量榜 TOP20（均价：￥{{total_avg_price}}）</span>
              </header>
              <div class="main_table t_btn8" style="margin-bottom: .6rem;">
                <table class="product_top20_table">
                  <thead>
                    <tr>
                      <th>排名</th>
                      <th>商品名称</th>
                      <th>类别</th>
                      <th>售量</th>
                      <th>均价</th>
                      <th>总卖量</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(item,index) in productCountTopTwenty" :key="index">
                      <td>{{index + 1}}</td>
                      <td>{{item.title}}</td>
                      <td>{{item.mainTag}}</td>
                      <td>{{item.monthSaleCount}}</td>
                      <td>￥{{item.price}}</td>
                      <td>{{item.saleCount}}</td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
            <div class="t_box" style=" height: auto;">
              <header class="t_title">
                <span>产品本月卖量榜 TOP20（均价：￥{{current_avg_price}}）</span>
              </header>
              <table class="product_top20_table" style="margin-bottom: .6rem;">
                <thead>
                  <tr>
                    <th>排名</th>
                    <th>商品名称</th>
                    <th>类别</th>
                    <th>售量</th>
                    <th>均价</th>
                    <th>总卖量</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(item,index) in currentMonthProductTopTwenty" :key="index">
                    <td>{{index + 1}}</td>
                    <td>{{item.title}}</td>
                    <td>{{item.mainTag}}</td>
                    <td>{{item.monthSaleCount}}</td>
                    <td>￥{{item.price}}</td>
                    <td>{{item.saleCount}}</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </li>
        </ul>
      </div>
      <shop></shop>
    </div>
  </div>
</template>
<script>
import test from "../../components/test";
import linegraph from "../../components/linegraph";
import wordcloud from "vue-wordcloud";
import echarts from "echarts";
import "../../../node_modules/echarts/map/js/province/beijing";

import shop from "../../components/shop";

import html2canvas from "html2canvas";

export default {
  components: {
    linegraph,
    wordcloud,
    test,
    shop
  },
  data() {
    return {
      show: true,
      shopCountOption: null,
      trisectionOption: null,
      decemberOption: null,

      shopOnlineCount: 0,
      shopCount: 0,
      orderCount: 0,
      saleMoneyCount: 0,

      commentOption: null,
      startOption: null,

      myColors: [
        "rgba(0,153,255,0.5)",
        "rgba(0,153,255,0.52)",
        "rgba(0,153,255,0.53)",
        "rgba(0,153,255,0.54)"
      ],
      /*月度行业指标详情 */
      data_x: null,
      comment_1_list: null,
      comment_2_list: null,
      comment_3_list: null,
      comment_4_list: null,
      comment_5_list: null,
      comment_count_list: null,

      shop_aptitude_list: null,
      shop_count_list: null,
      start_4_5_list: null,
      start_4_list: null,
      start_5_list: null,
      ym_hot_kw: null,
      /* 本月5星评论增加量门店排名 TOP20 */
      dianPingYmsTop: null,

      echart_product_type: null,
      chart_product_type_add: null,

      chart_product_sales_top5: null,
      chart_product_add_sales_top5: null,

      // 产品总销量榜 TOP20
      productCountTopTwenty: null,
      /* 产品总销量榜 TOP20 均价 */
      total_avg_price: null,
      current_avg_price: null,
      //   产品本月卖量榜  TOP20
      currentMonthProductTopTwenty: null,
      //月份
      month: null
    };
  },
  methods: {
    wordClickHandler(name, value, vm) {
      console.log("wordClickHandler", name, value, vm);
    },

    getDayNumByYearMonth(year, month) {
      switch (month) {
        case 1:
        case 3:
        case 5:
        case 7:
        case 8:
        case 10:
        case 12:
          return 31;
          break;
        case 4:
        case 6:
        case 9:
        case 11:
          return 30;
          break;
        case 2:
          return isLeapYear(year) ? 29 : 28;
          break;
      }
    },
    isLeapYear(year) {
      if (year / 4 == 0 && year / 100 != 0) {
        return true;
      } else if (year / 400 == 0) {
        return true;
      } else {
        return false;
      }
    },
    monthFun() {
      var yimeiform = sessionStorage.getItem("sendYimeiform");
      yimeiform = JSON.parse(yimeiform);
      let date = yimeiform.month;
      let year = date.substr(0, 4);
      let month = date.substr(5, 2);
  
      this.isLeapYear(year);
      this.getDayNumByYearMonth(year, month);
    },

    httpEcharts() {
      var yimeiform = sessionStorage.getItem("sendYimeiform");
      yimeiform = JSON.parse(yimeiform);
      console.log(yimeiform);
      var month = yimeiform.month;
      this.month = yimeiform.month;
      month = month.replace("年", "-");
      month = month.replace("月", "");
      console.log(month);
      this.$axios
        .post(
          `http://bi.doqtech.com.cn/dianping/ym/find/overview/${month}.json`
        )
        // .post("http://192.168.1.22:9595/dianping/ym/find/overview/2019-10.json")
        // .post("http://bi.doqtech.com.cn/dianping/ym/find/overview/2019-09.json")
        .then(res => {
          if ((res.data.status = 200)) {
            this.show = false;
          }
          console.log(res);
          //  热力图
          var date_X = res.data.data.date_X;

          // 本月门店趋势
          var amountTrend_X = res.data.data.amountTrend_X;
          var shopCount_Y = res.data.data.shopCount_Y;
          var shopOnlineCount_Y = res.data.data.shopOnlineCount_Y;

          var shopCountOption = {
            tooltip: {
              trigger: "axis",
              axisPointer: {
                type: "shadow"
              }
            },
            legend: {
              data: ["上线资质门店数", "门店数"],
              textStyle: {
                color: "rgba(255,255,255,.5)",
                fontSize: "16"
              }
            },
            grid: {
              left: "0%",
              top: "20%",
              right: "0%",
              bottom: "4%",
              containLabel: true
            },
            xAxis: [
              {
                type: "category",
                data: amountTrend_X,

                axisTick: {
                  show: false
                },
                axisLine: {
                  show: true,
                  lineStyle: {
                    color: "rgba(255,255,255,.1)",
                    width: 1,
                    type: "solid"
                  }
                },
                axisLabel: {
                  interval: 0,
                  // rotate:50,
                  show: true,
                  splitNumber: 15,
                  textStyle: {
                    color: "rgba(255,255,255,.6)",
                    fontSize: "16"
                  }
                }
              }
            ],
            yAxis: [
              {
                type: "value",
                axisLabel: {
                  //formatter: '{value} %'
                  show: true,
                  textStyle: {
                    color: "rgba(255,255,255,.6)",
                    fontSize: "16"
                  }
                },
                axisTick: {
                  show: false
                },
                axisLine: {
                  show: true,
                  lineStyle: {
                    color: "rgba(255,255,255,.1	)",
                    width: 1,
                    type: "solid"
                  }
                },
                splitLine: {
                  lineStyle: {
                    color: "rgba(255,255,255,.1)"
                  }
                }
              }
            ],
            series: [
              {
                name: "上线资质门店数",
                type: "bar",
                data: shopOnlineCount_Y,
                barWidth: "35%", //柱子宽度
                // barGap: 1, //柱子之间间距
                itemStyle: {
                  normal: {
                    color: "#2f89cf",
                    opacity: 1,
                    barBorderRadius: 5
                  }
                },
                label: {
                  normal: {
                    position: "top",
                    opacity: 1,
                    show: true,
                    rotate: "30"
                  }
                }
              },
              {
                name: "门店数",
                type: "bar",
                data: shopCount_Y,
                barWidth: "35%", //柱子宽度
                itemStyle: {
                  normal: {
                    color: "#27d08a",
                    opacity: 1,
                    barBorderRadius: 5
                  }
                },
                label: {
                  normal: {
                    position: "top",
                    opacity: 1,
                    show: true,
                    rotate: "30"
                  }
                }
              }
            ]
          };
          this.shopCountOption = shopCountOption;

          // 三分（效果，环境，服务）
          var score_X = res.data.data.score_X;
          var env_score_Y = res.data.data.env_score_Y;
          var quality_score_Y = res.data.data.quality_score_Y;
          var service_score_Y = res.data.data.service_score_Y;
          var trisectionOption = {
            tooltip: {
              trigger: "axis",
              axisPointer: { type: "shadow" }
            },
            legend: {
              top: "0%",
              data: ["效果", "环境", "服务"],
              textStyle: {
                color: "rgba(255,255,255,.5)",
                fontSize: "16"
              }
            },
            grid: {
              left: "0%",
              top: "20%",
              right: "0%",
              bottom: "4%",
              containLabel: true
            },
            xAxis: [
              {
                type: "category",
                data: score_X,
                axisLine: {
                  show: true,
                  lineStyle: {
                    color: "rgba(255,255,255,.1)",
                    width: 1,
                    type: "solid"
                  }
                },

                axisTick: {
                  show: false
                },
                axisLabel: {
                  interval: 0,
                  // rotate:50,
                  show: true,
                  splitNumber: 15,
                  textStyle: {
                    color: "rgba(255,255,255,0.6)",
                    fontSize: "16"
                  }
                }
              }
            ],
            yAxis: [
              {
                type: "value",
                axisLabel: {
                  show: true,
                  textStyle: {
                    color: "rgba(255,255,255,0.6)",
                    fontSize: "16"
                  }
                },
                axisTick: {
                  show: false
                },
                axisLine: {
                  show: true,
                  lineStyle: {
                    color: "rgba(255,255,255,0.1)",
                    width: 1,
                    type: "solid"
                  }
                },
                splitLine: {
                  lineStyle: {
                    color: "rgba(255,255,255,0.1)"
                  }
                }
              }
            ],
            series: [
              {
                name: "效果",
                type: "bar",
                data: quality_score_Y,
                barWidth: "15%", //柱子宽度
                // barGap: 1, //柱子之间间距
                itemStyle: {
                  normal: {
                    color: "#8dc63f",
                    opacity: 1,
                    barBorderRadius: 5
                  }
                },
                label: {
                  normal: {
                    position: "top",
                    opacity: 1,
                    show: true,
                    rotate: "60"
                  }
                }
              },
              {
                name: "环境",
                type: "bar",
                data: env_score_Y,
                barWidth: "15%", //柱子宽度
                // barGap: 1, //柱子之间间距
                itemStyle: {
                  normal: {
                    color: "#fbbd08",
                    opacity: 1,
                    barBorderRadius: 5
                  }
                },
                label: {
                  normal: {
                    position: "top",
                    opacity: 1,
                    show: true,
                    rotate: "60"
                  }
                }
              },
              {
                name: "服务",
                type: "bar",
                data: service_score_Y,
                barWidth: "15%", //柱子宽度
                // barGap: 1, //柱子之间间距
                itemStyle: {
                  normal: {
                    color: "#f37b1d",
                    opacity: 1,
                    barBorderRadius: 5
                  }
                },
                label: {
                  normal: {
                    position: "top",
                    opacity: 1,
                    show: true,
                    rotate: "60"
                  }
                }
              }
            ]
          };
          this.trisectionOption = trisectionOption;

          //  近十二月首评分布
          var first_comment_X = res.data.data.first_comment_X;
          var first_comment_Y = res.data.data.first_comment_Y;
          console.log(first_comment_X);
          var decemberOption = {
            tooltip: {
              trigger: "axis",
              axisPointer: {
                lineStyle: {
                  color: "#dddc6b"
                }
              }
            },
            legend: {
              top: "0%",
              textStyle: {
                color: "rgba(255,255,255,.5)",
                fontSize: "16"
              }
            },
            grid: {
              left: "12",
              top: "30",
              right: "10",
              bottom: "10",
              containLabel: true
            },

            xAxis: [
              {
                type: "category",
                nameRotate: "40",
                boundaryGap: false,
                axisLabel: {
                  interval: 0,
                  nameRotate: "40"
                },
                axisLabel: {
                  show: true,
                  rotate: "30"
                },

                axisLine: {
                  lineStyle: {
                    color: "rgba(255,255,255,.2)"
                  }
                },

                data: first_comment_X
              },
              {
                axisPointer: { show: false },
                axisLine: { show: false },
                position: "bottom",
                offset: 20
              }
            ],

            yAxis: [
              {
                type: "value",
                axisTick: { show: false },
                axisLine: {
                  lineStyle: {
                    color: "rgba(255,255,255,.1)"
                  }
                },
                axisLabel: {
                  textStyle: {
                    color: "rgba(255,255,255,.6)",
                    fontSize: 16
                  }
                },

                splitLine: {
                  lineStyle: {
                    color: "rgba(255,255,255,.1)"
                  }
                }
              }
            ],
            series: [
              {
                // name: "首评分布",
                type: "line",
                smooth: true,
                symbol: "circle",
                symbolSize: 5,
                showSymbol: false,
                lineStyle: {
                  normal: {
                    color: "#0184d5",
                    width: 2
                  }
                },
                areaStyle: {
                  normal: {
                    color:
                      (0,
                      0,
                      0,
                      1,
                      [
                        {
                          offset: 0,
                          color: "rgba(1, 132, 213, 0.4)"
                        },
                        {
                          offset: 0.8,
                          color: "rgba(1, 132, 213, 0.1)"
                        }
                      ],
                      false),
                    shadowColor: "rgba(0, 0, 0, 0.1)"
                  }
                },

                itemStyle: {
                  normal: {
                    color: "#0184d5",
                    borderColor: "rgba(100, 100, 100, .1)",
                    borderWidth: 12
                  }
                },
                data: first_comment_Y
              }
            ]
          };
          this.decemberOption = decemberOption;

          // 本月具备上线
          var shopCount = res.data.data.shopCount;
          this.shopCount = res.data.data.shopCount;

          //本月总门店数
          var shopOnlineCount = res.data.data.shopOnlineCount;
          this.shopOnlineCount = res.data.data.shopOnlineCount;

          //本月总订单数
          var orderCount = res.data.data.orderCount;
          this.orderCount = orderCount;

          //本月总销量额
          var saleMoneyCount = res.data.data.saleMoneyCount;
          this.saleMoneyCount = saleMoneyCount;

          //月度好评/差评
          var comment_X = res.data.data.comment_X;
          var bad_comment_Y = res.data.data.bad_comment_Y;
          var good_comment_Y = res.data.data.good_comment_Y;

          var commentOption = {
            tooltip: {
              trigger: "axis",
              axisPointer: {
                lineStyle: {
                  color: "#dddc6b"
                }
              }
            },
            legend: {
              top: "0%",
              data: ["好评数", "中差评数"],
              textStyle: {
                color: "rgba(255,255,255,.5)",
                fontSize: "16"
              }
            },
            grid: {
              left: "10",
              top: "30",
              right: "10",
              bottom: "10",
              containLabel: true
            },

            xAxis: [
              {
                type: "category",
                boundaryGap: false,
                axisLabel: {
                  textStyle: {
                    color: "rgba(255,255,255,.6)",
                    fontSize: 16
                  }
                },
                axisLine: {
                  lineStyle: {
                    color: "rgba(255,255,255,.2)"
                  }
                },

                data: comment_X
              },
              {
                axisPointer: { show: false },
                axisLine: { show: false },
                position: "bottom",
                offset: 20
              }
            ],

            yAxis: [
              {
                type: "value",
                axisTick: { show: false },
                axisLine: {
                  lineStyle: {
                    color: "rgba(255,255,255,.1)"
                  }
                },
                axisLabel: {
                  textStyle: {
                    color: "rgba(255,255,255,.6)",
                    fontSize: 16
                  }
                },

                splitLine: {
                  lineStyle: {
                    color: "rgba(255,255,255,.1)"
                  }
                }
              }
            ],
            series: [
              {
                name: "好评数",
                type: "line",
                symbol: "circle",
                symbolSize: 5,
                showSymbol: false,
                lineStyle: {
                  normal: {
                    color: "#0184d5",
                    width: 2
                  }
                },
                areaStyle: {
                  normal: {
                    color:
                      (0,
                      0,
                      0,
                      1,
                      [
                        { offset: 0, color: "rgba(1, 132, 213, 0.4)" },
                        { offset: 0.8, color: "rgba(1, 132, 213, 0.1)" }
                      ],
                      false),
                    shadowColor: "rgba(0, 0, 0, 0.1)"
                  }
                },
                itemStyle: {
                  normal: {
                    color: "#0184d5",
                    borderColor: "rgba(221, 220, 107, .1)",
                    borderWidth: 12
                  }
                },
                data: good_comment_Y
              },
              {
                name: "中差评数",
                type: "line",
                smooth: true,
                symbol: "circle",
                symbolSize: 5,
                showSymbol: false,
                lineStyle: {
                  normal: {
                    color: "#00d887",
                    width: 2
                  }
                },
                areaStyle: {
                  normal: {
                    color:
                      (0,
                      0,
                      0,
                      1,
                      [
                        { offset: 0, color: "rgba(0, 216, 135, 0.4)" },
                        { offset: 0.8, color: "rgba(0, 216, 135, 0.1)" }
                      ],
                      false),
                    shadowColor: "rgba(0, 0, 0, 0.1)"
                  }
                },
                itemStyle: {
                  normal: {
                    color: "#00d887",
                    borderColor: "rgba(221, 220, 107, .1)",
                    borderWidth: 12
                  }
                },
                data: bad_comment_Y
              }
            ]
          };
          this.commentOption = commentOption;

          // 星级门店分布
          var start_X = res.data.data.start_X;
          var start_count_Y = res.data.data.start_count_Y;
          var startOption = {
            tooltip: {
              trigger: "axis",
              axisPointer: {
                type: "shadow"
              }
            },

            grid: {
              left: "0%",
              top: "10px",
              right: "0%",
              bottom: "2%",
              containLabel: true
            },
            xAxis: [
              {
                type: "category",
                data: start_X,
                axisLine: {
                  show: true,
                  lineStyle: {
                    color: "rgba(255,255,255,.1)",
                    width: 1,
                    type: "solid"
                  }
                },

                axisTick: {
                  show: false
                },
                axisLabel: {
                  interval: 0,
                  // rotate:50,
                  show: true,
                  splitNumber: 15,
                  textStyle: {
                    color: "rgba(255,255,255,.6)",
                    fontSize: "16"
                  }
                }
              }
            ],
            yAxis: [
              {
                type: "value",
                axisLabel: {
                  //formatter: '{value} %'
                  show: true,
                  textStyle: {
                    color: "rgba(255,255,255,.6)",
                    fontSize: "16"
                  }
                },
                axisTick: {
                  show: false
                },
                axisLine: {
                  show: true,
                  lineStyle: {
                    color: "rgba(255,255,255,.1	)",
                    width: 1,
                    type: "solid"
                  }
                },
                splitLine: {
                  lineStyle: {
                    color: "rgba(255,255,255,.1)"
                  }
                }
              }
            ],
            series: [
              {
                type: "bar",
                data: start_count_Y,
                barWidth: "35%", //柱子宽度
                // barGap: 1, //柱子之间间距
                itemStyle: {
                  normal: {
                    color: "#2f89cf",
                    opacity: 1,
                    barBorderRadius: 5
                  }
                },
                label: {
                  position: "top",
                  opacity: 1,
                  show: true,
                  rotate: "30"
                }
              }
            ]
          };
          this.startOption = startOption;

          // 热搜词
          var ym_hot_kw = res.data.data.ym_hot_kw;
          this.ym_hot_kw = ym_hot_kw;

          //  日期
          var data_x = res.data.data.data_x;
          this.data_x = data_x;

          /*月度行业指标详情 */
          var comment_1_list = res.data.data.comment_1_list;
          this.comment_1_list = comment_1_list;
          var comment_2_list = res.data.data.comment_2_list;
          this.comment_2_list = comment_2_list;
          var comment_3_list = res.data.data.comment_3_list;
          this.comment_3_list = comment_3_list;
          var comment_4_list = res.data.data.comment_4_list;
          this.comment_4_list = comment_4_list;
          var comment_5_list = res.data.data.comment_5_list;
          this.comment_5_list = comment_5_list;
          var comment_count_list = res.data.data.comment_count_list;
          this.comment_count_list = comment_count_list;
          var data_x = res.data.data.data_x;
          this.data_x = data_x;
          var shop_aptitude_list = res.data.data.shop_aptitude_list;
          this.shop_aptitude_list = shop_aptitude_list;
          var shop_count_list = res.data.data.shop_count_list;
          this.shop_count_list = shop_count_list;
          var start_4_5_list = res.data.data.start_4_5_list;
          this.start_4_5_list = start_4_5_list;
          var start_4_list = res.data.data.start_4_list;
          this.start_4_list = start_4_list;
          var start_5_list = res.data.data.start_5_list;
          this.start_5_list = start_5_list;

          /* 本月5星评论增加量门店排名 TOP20 */
          var dianPingYmsTopqian = res.data.data.dianPingYmsTop;
          console.log(dianPingYmsTopqian);
          var dianPingYmsTop = new Array();
          for (let i = 0; i < dianPingYmsTopqian.length; i++) {
            var id = dianPingYmsTopqian[i].id;
            var defaultPic = dianPingYmsTopqian[i].defaultPic;
            var name = dianPingYmsTopqian[i].name;
            var start_5_add = dianPingYmsTopqian[i].start_5_add;
            var address = dianPingYmsTopqian[i].address;
            var phoneNum = dianPingYmsTopqian[i].phoneNum;
            phoneNum = phoneNum.substr(0, phoneNum.length - 1);
            var shopPower = dianPingYmsTopqian[i].shopPower;
            shopPower = shopPower / 10;
            var envScore = dianPingYmsTopqian[i].envScore;
            var qualityScore = dianPingYmsTopqian[i].qualityScore;
            var serviceScore = dianPingYmsTopqian[i].serviceScore;
            var product_count = dianPingYmsTopqian[i].product_count;
            var orderCount = dianPingYmsTopqian[i].orderCount;
            var monthOrderCount = dianPingYmsTopqian[i].monthOrderCount;
            var reviewCount = dianPingYmsTopqian[i].reviewCount;
            var obj = new Object();
            obj.id = id;
            obj.defaultPic = defaultPic;
            obj.name = name;
            obj.start_5_add = start_5_add;
            obj.address = address;
            obj.phoneNum = phoneNum;
            obj.shopPower = shopPower;
            obj.envScore = envScore;
            obj.qualityScore = qualityScore;
            obj.serviceScore = serviceScore;
            obj.product_count = product_count;
            obj.orderCount = orderCount;
            obj.monthOrderCount = monthOrderCount;
            obj.reviewCount = reviewCount;
            dianPingYmsTop.push(obj);
          }

          this.dianPingYmsTop = dianPingYmsTop;

          /* 品种类总卖量排名 TOP10 */

          var monthDataList_zhexian_X = res.data.data.monthDataList_zhexian_X;
          var monthDataList_zhexian_Y = res.data.data.monthDataList_zhexian_Y;
          var monthDataList_bingtu = res.data.data.monthDataList_bingtu;
          var echart_product_type = {
            graphic: {
              elements: [
                {
                  type: "image",
                  style: {
                    image:
                      "data:image/png;base64,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",
                    width: 30,
                    height: 30
                  },
                  left: "73%",
                  top: "center"
                }
              ]
            },
            tooltip: {
              trigger: "axis",
              axisPointer: {
                type: "shadow"
              }
            },
            legend: {
              data: ["销量"],
              left: "27%"
            },
            grid: {
              left: "1%",
              right: "60%",
              top: "10%",
              bottom: "10%",
              containLabel: true
            },
            xAxis: {
              type: "value",
              position: "top",
              splitLine: { show: false },
              boundaryGap: [0, 0.01],
              axisTick: {
                show: false
              },
              axisLabel: {
                show: true,
                rotate: "45",
                textStyle: {
                  color: "#9ea7c4",
                  fontSize: 12
                }
              },
              axisLine: {
                show: true,
                lineStyle: {
                  color: "#6173A3"
                }
              }
            },
            yAxis: {
              type: "category",
              data: monthDataList_zhexian_Y,
              axisTick: {
                show: false
              },
              splitLine: {
                show: false
              },
              axisLabel: {
                textStyle: {
                  color: "#9ea7c4",
                  fontSize: 16
                }
              },
              axisLine: {
                show: true,
                lineStyle: {
                  color: "#6173A3"
                }
              }
            },
            series: [
              {
                name: "",
                itemStyle: {
                  normal: {
                    show: true,
                    color: function(params) {
                      // build a color map as your need.
                      var colorList = [
                        "#C1232B",
                        "#B5C334",
                        "#FCCE10",
                        "#E87C25",
                        "#27727B",
                        "#FE8463",
                        "#9BCA63",
                        "#FAD860",
                        "#F3A43B",
                        "#60C0DD",
                        "#D7504B",
                        "#C6E579",
                        "#F4E001",
                        "#F0805A",
                        "#26C0C0"
                      ];
                      return colorList[params.dataIndex];
                    },
                    shadowBlur: 16,

                    shadowColor: "rgba(0, 0, 0, 0.5)"
                  }
                },
                label: {
                  normal: {
                    position: "right",
                    show: true
                  }
                },
                type: "bar",
                data: monthDataList_zhexian_X
              },
              {
                type: "pie",
                radius: [30, "60%"],
                center: ["69%", "50%"],
                roseType: "radius",
                color: [
                  "#C1232B",
                  "#B5C334",
                  "#FCCE10",
                  "#E87C25",
                  "#27727B",
                  "#FE8463",
                  "#9BCA63",
                  "#FAD860",
                  "#F3A43B",
                  "#60C0DD",
                  "#D7504B",
                  "#C6E579",
                  "#F4E001",
                  "#F0805A",
                  "#26C0C0"
                ],
                data: monthDataList_bingtu,
                label: {
                  normal: {
                    textStyle: {
                      fontSize: 16
                    },
                    formatter: function(param) {
                      return (
                        param.name + "：" + Math.round(param.percent) + "%"
                      );
                    }
                  }
                },
                labelLine: {
                  normal: {
                    smooth: true,
                    lineStyle: {
                      width: 2
                    }
                  }
                },
                itemStyle: {
                  normal: {
                    shadowBlur: 16,
                    shadowColor: "rgba(0, 0, 0, 0.4)"
                  }
                },

                animationType: "scale",
                animationEasing: "elasticOut",
                animationDelay: function(idx) {
                  return Math.random() * 100;
                }
              }
            ]
          };
          this.echart_product_type = echart_product_type;

          /* 本月品种类卖量排名 TOP10 */
          var totalDataList_zhexian_X = res.data.data.totalDataList_zhexian_X;
          var totalDataList_zhexian_Y = res.data.data.totalDataList_zhexian_Y;
          var totalDataList_bingtu = res.data.data.totalDataList_bingtu;

          var chart_product_type_add = {
            graphic: {
              elements: [
                {
                  type: "image",
                  style: {
                    image:
                      "data:image/png;base64,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",
                    width: 30,
                    height: 30
                  },
                  left: "73%",
                  top: "center"
                }
              ]
            },
            tooltip: {
              trigger: "axis",
              axisPointer: {
                type: "shadow"
              }
            },
            legend: {
              data: ["销售额"],
              left: "27%"
            },
            grid: {
              left: "1%",
              right: "60%",
              top: "10%",
              bottom: "10%",
              containLabel: true
            },
            xAxis: {
              type: "value",
              position: "top",
              splitLine: { show: false },
              boundaryGap: [0, 0.01],
              axisTick: {
                show: false
              },
              axisLabel: {
                show: true,
                rotate: "45",
                textStyle: {
                  color: "#9ea7c4",
                  fontSize: 16
                }
              },
              axisLine: {
                show: true,
                lineStyle: {
                  color: "#6173A3"
                }
              }
            },
            yAxis: {
              type: "category",
              data: totalDataList_zhexian_Y,
              axisTick: {
                show: false
              },
              splitLine: {
                show: false
              },
              axisLabel: {
                textStyle: {
                  color: "#9ea7c4",
                  fontSize: 16
                }
              },
              axisLine: {
                show: true,
                lineStyle: {
                  color: "#6173A3"
                }
              }
            },
            series: [
              {
                name: "",
                itemStyle: {
                  normal: {
                    color: function(params) {
                      // build a color map as your need.
                      var colorList = [
                        "#C1232B",
                        "#B5C334",
                        "#FCCE10",
                        "#E87C25",
                        "#27727B",
                        "#FE8463",
                        "#9BCA63",
                        "#FAD860",
                        "#F3A43B",
                        "#60C0DD",
                        "#D7504B",
                        "#C6E579",
                        "#F4E001",
                        "#F0805A",
                        "#26C0C0"
                      ];
                      return colorList[params.dataIndex];
                    },
                    shadowBlur: 16,
                    shadowColor: "rgba(0, 0, 0, 0.5)"
                  }
                },
                label: {
                  normal: {
                    position: "right",
                    show: true
                  }
                },
                type: "bar",
                data: totalDataList_zhexian_X
              },
              {
                type: "pie",
                radius: [30, "60%"],
                center: ["69%", "50%"],
                roseType: "radius",
                color: [
                  "#C1232B",
                  "#B5C334",
                  "#FCCE10",
                  "#E87C25",
                  "#27727B",
                  "#FE8463",
                  "#9BCA63",
                  "#FAD860",
                  "#F3A43B",
                  "#60C0DD",
                  "#D7504B",
                  "#C6E579",
                  "#F4E001",
                  "#F0805A",
                  "#26C0C0"
                ],
                data: totalDataList_bingtu,
                label: {
                  normal: {
                    textStyle: {
                      fontSize: 16
                    },
                    formatter: function(param) {
                      return (
                        param.name + "：" + Math.round(param.percent) + "%"
                      );
                    }
                  }
                },
                labelLine: {
                  normal: {
                    smooth: true,
                    lineStyle: {
                      width: 2
                    }
                  }
                },
                itemStyle: {
                  normal: {
                    shadowBlur: 16,
                    shadowColor: "rgba(0, 0, 0, 0.4)"
                  }
                },

                animationType: "scale",
                animationEasing: "elasticOut",
                animationDelay: function(idx) {
                  return Math.random() * 200;
                }
              }
            ]
          };
          this.chart_product_type_add = chart_product_type_add;

          // TOP5种类总卖量变化曲线图
          var totalCountTopTagName = res.data.data.totalCountTopTagName;
          var totalCountTop1 = res.data.data.totalCountTop1;
          var totalCountTop2 = res.data.data.totalCountTop2;
          var totalCountTop3 = res.data.data.totalCountTop3;
          var totalCountTop4 = res.data.data.totalCountTop4;
          var totalCountTop5 = res.data.data.totalCountTop5;
          var chart_product_sales_top5 = {
            title: [
              {
                text: "",
                left: "93%",
                top: "15%",
                textAlign: "center",
                textStyle: {
                  color: "#fff",
                  fontSize: "14"
                }
              }
            ],
            tooltip: {
              trigger: "axis"
            },
            legend: {
              x: 300,
              top: "5%",
              left: "center",
              textStyle: {
                color: "#ffd285"
              },
              data: totalCountTopTagName
            },
            grid: {
              left: "1%",
              right: "5%",
              top: "26%",
              bottom: "1%",
              containLabel: true
            },
            toolbox: {
              show: false,
              feature: {
                saveAsImage: {}
              }
            },
            xAxis: [
              {
                type: "category",
                boundaryGap: false,
                axisLabel: {
                  textStyle: {
                    color: "#fff"
                  }
                },
                axisLine: {
                  lineStyle: {
                    color: "#fff"
                  }
                },

                data: comment_X
              },
              {
                axisPointer: { show: false },
                axisLine: { show: false },
                position: "bottom",
                offset: 20
              }
            ],
            yAxis: {
              axisLine: {
                lineStyle: {
                  color: "#fff"
                }
              },
              splitLine: {
                show: false,
                lineStyle: {
                  color: "#fff"
                }
              },
              axisTick: {
                show: true
              },
              axisLabel: {
                show: true,
                textStyle: {
                  color: "#fff"
                }
              },
              label: {
                show: true
              },
              type: "value"
            },
            series: [
              {
                name: totalCountTopTagName[0],
                smooth: true,
                type: "line",
                symbolSize: 9,
                lineStyle: {
                  color: "#C1232B"
                },
                symbol: "circle",
                data: totalCountTop1
              },
              {
                name: totalCountTopTagName[1],
                smooth: true,
                type: "line",
                symbolSize: 9,
                lineStyle: {
                  color: "#B5C334"
                },
                symbol: "circle",
                data: totalCountTop2
              },
              {
                name: totalCountTopTagName[2],
                smooth: true,
                type: "line",
                lineStyle: {
                  color: "#FCCE10"
                },
                symbolSize: 9,
                symbol: "circle",
                data: totalCountTop3
              },
              {
                name: totalCountTopTagName[3],
                smooth: true,
                type: "line",
                lineStyle: {
                  color: "#E87C25"
                },
                symbolSize: 9,
                symbol: "circle",
                data: totalCountTop4
              },
              {
                name: totalCountTopTagName[4],
                smooth: true,
                type: "line",
                lineStyle: {
                  color: "#27727B"
                },
                symbolSize: 9,
                symbol: "circle",
                data: totalCountTop5
              }
            ]
          };
          this.chart_product_sales_top5 = chart_product_sales_top5;
          //TOP5种类本月卖量变化曲线图
          var currentMonthCountTopTagName =
            res.data.data.currentMonthCountTopTagName;
          var currentMonthCountTop1 = res.data.data.currentMonthCountTop1;
          var currentMonthCountTop2 = res.data.data.currentMonthCountTop2;
          var currentMonthCountTop3 = res.data.data.currentMonthCountTop3;
          var currentMonthCountTop4 = res.data.data.currentMonthCountTop4;
          var currentMonthCountTop5 = res.data.data.currentMonthCountTop5;
          var chart_product_add_sales_top5 = {
            title: [
              {
                text: "",
                left: "1%",
                top: "15%",
                textStyle: {
                  color: "#fff"
                }
              },
              {
                text: "",
                left: "93%",
                top: "15%",
                textAlign: "center",
                textStyle: {
                  color: "#fff",
                  fontSize: 16
                }
              }
            ],
            tooltip: {
              trigger: "axis"
            },
            legend: {
              x: 300,
              top: "5%",
              left: "center",
              textStyle: {
                color: "#ffd285"
              },
              data: currentMonthCountTopTagName
            },
            grid: {
              left: "1%",
              right: "5%",
              top: "26%",
              bottom: "1%",
              containLabel: true
            },
            toolbox: {
              show: false,
              feature: {
                saveAsImage: {}
              }
            },
            xAxis: [
              {
                type: "category",
                boundaryGap: false,
                axisLabel: {
                  textStyle: {
                    color: "#fff"
                  }
                },
                axisLine: {
                  lineStyle: {
                    color: "#fff"
                  }
                },

                data: comment_X
              },
              {
                axisPointer: { show: false },
                axisLine: { show: false },
                position: "bottom",
                offset: 20
              }
            ],
            yAxis: {
              axisLine: {
                lineStyle: {
                  color: "#fff"
                }
              },
              splitLine: {
                show: false,
                lineStyle: {
                  color: "#fff"
                }
              },
              axisTick: {
                show: true
              },
              axisLabel: {
                textStyle: {
                  color: "#fff"
                }
              },
              type: "value"
            },
            series: [
              {
                name: currentMonthCountTopTagName[0],
                smooth: true,
                type: "line",
                symbolSize: 9,
                symbol: "circle",
                lineStyle: {
                  color: "#C1232B"
                },
                data: currentMonthCountTop1
              },
              {
                name: currentMonthCountTopTagName[1],
                smooth: true,
                type: "line",
                symbolSize: 9,
                symbol: "circle",
                lineStyle: {
                  color: "#B5C334"
                },
                data: currentMonthCountTop2
              },
              {
                name: currentMonthCountTopTagName[2],
                smooth: true,
                type: "line",
                symbolSize: 9,
                symbol: "circle",
                lineStyle: {
                  color: "#FCCE10"
                },
                data: currentMonthCountTop3
              },
              {
                name: currentMonthCountTopTagName[3],
                smooth: true,
                type: "line",
                symbolSize: 9,
                symbol: "circle",
                lineStyle: {
                  color: "#E87C25"
                },
                data: currentMonthCountTop4
              },
              {
                name: currentMonthCountTopTagName[4],
                smooth: true,
                type: "line",
                symbolSize: 9,
                symbol: "circle",
                lineStyle: {
                  color: "#27727B"
                },
                data: currentMonthCountTop4
              }
            ]
          };
          this.chart_product_add_sales_top5 = chart_product_add_sales_top5;

          // 产品总销量榜 TOP20
          var productCountTopTwenty = res.data.data.productCountTopTwenty;
          this.productCountTopTwenty = productCountTopTwenty;
          /* 产品总销量榜 TOP20 均价 */
          var total_avg_price = res.data.data.total_avg_price;
          this.total_avg_price = total_avg_price;
          var current_avg_price = res.data.data.current_avg_price;
          this.current_avg_price = current_avg_price;

          var currentMonthProductTopTwenty =
            res.data.data.currentMonthProductTopTwenty;
          this.currentMonthProductTopTwenty = currentMonthProductTopTwenty;

          var locationNameMap = res.data.data.locationNameMap;
          var dataMap = res.data.data.locationNameMap;

          var geoCoordMap = res.data.data.locationMap;
          var convertData = function(dataMap) {
            var res = [];
            for (var i = 0; i < dataMap.length; i++) {
              var geoCoord = geoCoordMap[dataMap[i].name];
              if (geoCoord) {
                res.push({
                  name: dataMap[i].name,
                  value: geoCoord.concat(dataMap[i].value)
                });
              }
            }
            return res;
          };

          let mapOption = {
            tooltip: {
              trigger: "item",
              formatter: function(params) {
                if (typeof params.value[2] == "undefined") {
                  return params.name + " : " + params.value;
                } else {
                  return params.name + " : " + params.value[2];
                }
              }
            },
            visualMap: {
              min: 0,
              max: 500,
              show: false,
              splitNumber: 5,
              inRange: {
                color: ["#d94e5d", "#eac736", "#50a3ba"].reverse()
              },
              textStyle: {
                color: "#fff"
              }
            },
            geo: {
              map: "北京",
              label: {
                normal: {
                  show: true,
                  color: "#fff"
                },
                emphasis: {
                  show: true,
                  color: "#fff"
                }
              },
              roam: false,
              itemStyle: {
                normal: {
                  areaColor: "#40458e",
                  borderColor: "#6367ad",
                  borderWidth: 1.5
                },
                emphasis: {
                  areaColor: "#40458e"
                }
              },
              left: 0,
              right: 0,
              top: 0,
              bottom: 0
            },
            series: [
              {
                name: "门店数量",
                type: "scatter",
                coordinateSystem: "geo",
                data: convertData(dataMap),
                symbolSize: function(val) {
                  return val[2] / 0.2;
                },
                label: {
                  normal: {
                    formatter: "{b}",
                    position: "right",
                    show: false
                  },
                  emphasis: {
                    show: true
                  }
                },
                itemStyle: {
                  normal: {
                    color: "#ffeb7b"
                  }
                }
              }
            ]
          };

          this.mapOption = mapOption;
        })
        .catch(err => {
          console.log(err);
        });
    }
  },
  created() {
    this.httpEcharts();
    this.monthFun();
  }
};
</script>

<style rel="scss" lang="scss" scoped>
@import "../../assets/style/medicine.css";
@import "../../assets/style/font.css";
</style>