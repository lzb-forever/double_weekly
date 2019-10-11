<template>
  <div>
    <div class="mainbox">
      <div class="caption-title">
        <i>
          <img src="../assets/img/medicne/title-left.png" />
        </i>
        <span class="biaoti">{{shopName}} 门店指标概览</span>
        <i>
          <img src="../assets/img/medicne/title-right.png" />
        </i>
      </div>
      <ul class="clearfix" style="width: 99%;margin:0 auto">
        <li style="width: 100%; display: flex;">
          <div class="t_mbox t_ybox">
            <i></i>
            <span>本月团购卖量</span>
            <h2>{{tuangou_mailiang}}</h2>
          </div>
          <div class="t_mbox t_gbox">
            <i></i>
            <span>本月新增评论数</span>
            <h2>{{new_add_comment}}</h2>
          </div>
          <div class="t_mbox t_rbox">
            <i></i>
            <span>门店人均消费</span>
            <h2>￥{{avg_consume}}</h2>
          </div>

          <div class="t_mbox t_start">
            <i></i>
            <span>当前门店星级</span>
            <h2>{{start_rank}}</h2>
          </div>

          <div
            class="t_mbox"
            style="width:5rem; display: flex;flex-direction: column;align-items: center;justify-content: center; background-color: coral;"
          >
            <span style="left: 2%; top:2%;">当前门店评分</span>
            <div class="score-group">
              <div class="score-item">
                <label>效果：</label>
                <h3>{{env_score}}</h3>
              </div>
              <div class="score-item">
                <label>环境：</label>
                <h3>{{service_score}}</h3>
              </div>
              <div class="score-item">
                <label>服务：</label>
                <h3>{{quality_score}}</h3>
              </div>
            </div>
          </div>
        </li>
        <li style="width: 100%; display: flex; margin-top:.5rem; height: 475px; ">
          <div class="user_left l_left" style="margin-right: .2rem;">
            <div class="user_line1">
              <div class="user_line2">
                <div class="user_top_middle">
                  <p>门店本月评论数走势图</p>
                  <linegraph
                    class="allnav"
                    :id="'bargraph11'"
                    :data="showShopComment"
                    style="height:400px; width: 98%"
                  ></linegraph>
                </div>
              </div>
            </div>
          </div>

          <div class="user_left l_left">
            <div class="user_line1">
              <div class="user_line2">
                <div class="user_top_middle">
                  <p>本月门店3分变化情况</p>
                  <linegraph
                    class="allnav"
                    :id="'bargraph12'"
                    :data="shop3Score"
                    style="height:400px; width: 98%"
                  ></linegraph>
                </div>
              </div>
            </div>
          </div>
        </li>
        <li class="w100" style="margin-top: .4rem;">
          <div class="alltitle">门店本月人气榜排名详情</div>
          <table class="t_table">
            <thead>
              <tr>
                <th>{{month}}</th>
                <th v-for="(item,index) in date_X" :key="index">{{item}}</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td style="width: 100px;">好评榜排名</td>
                <td v-for="(item,index) in haoping_Y" :key="index">{{item}}</td>
              </tr>
              <tr>
                <td>效果最佳排名</td>
                <td v-for="(item,index) in xiaoguo_y" :key="index">{{item}}</td>
              </tr>
              <tr>
                <td>环境最佳排名</td>
                <td v-for="(item,index) in huangjing_Y" :key="index">{{item}}</td>
              </tr>
              <tr>
                <td>服务最佳排名</td>
                <td v-for="(item,index) in fuwu_Y" :key="index">{{item}}</td>
              </tr>
              <tr>
                <td>低价优先排名</td>
                <td v-for="(item,index) in dijia_Y" :key="index">{{item}}</td>
              </tr>
              <tr>
                <td>高价优先排名</td>
                <td v-for="(item,index) in gaojia_Y" :key="index">{{item}}</td>
              </tr>
            </tbody>
          </table>
        </li>
      </ul>

      <div class="data">
        <div class="data-title">
          <div class="title-left fl"></div>
          <div class="title-center fl">门店产品指标概览</div>
          <div class="title-right fr"></div>
        </div>
      </div>
      <ul class="clearfix">
        <li class="w100" style="display: flex; align-items: center; justify-content: center;">
          <div class="cen-bottom" style="width: 50%; height:auto; margin-right: .2rem;">
            <div class="title">种类销量排名榜 TOP10</div>
            <img src="../assets/img/medicne/bj-1.png" alt class="bj-1" />
            <img src="../assets/img/medicne/bj-2.png" alt class="bj-2" />
            <img src="../assets/img/medicne/bj-3.png" alt class="bj-3" />
            <img src="../assets/img/medicne/bj-4.png" alt class="bj-4" />
            <linegraph
              class="allnav"
              :id="'bargraph15'"
              :data="echart_product_type_shop"
              style="height:400px; width: 98%"
            ></linegraph>

            <div class="title">产品总销量排名 TOP10（均价：￥{{total_avg_price}}）</div>
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
                  <tr v-for="(item,index) in productCountTopTen" :key="index">
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

          <div class="cen-bottom" style="width: 50%; height: auto">
            <div class="title">各种类本月卖量排名榜 TOP10</div>
            <img src="../assets/img/medicne/bj-1.png" alt class="bj-1" />
            <img src="../assets/img/medicne/bj-2.png" alt class="bj-2" />
            <img src="../assets/img/medicne/bj-3.png" alt class="bj-3" />
            <img src="../assets/img/medicne/bj-4.png" alt class="bj-4" />
            <linegraph
              class="allnav"
              :id="'bargraph16'"
              :data="echart_product_type_shop_add"
              style="height:400px; width: 98%, "
            ></linegraph>

            <div class="title">产品本月销量排名 TOP10（均价：￥{{current_avg_price}}）</div>
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
                  <tr v-for="(item,index) in currentMonthProductTopTen" :key="index">
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
        </li>

        <li
          class="w100"
          style="margin-top: .3rem; display: flex; align-items: center; justify-content: center;"
        >
          <div class="cen-bottom" style="height: auto; width:99%;margin:0 auto;">
            <img src="../assets/img/medicne/bj-1.png" alt class="bj-1" />
            <img src="../assets/img/medicne/bj-2.png" alt class="bj-2" />
            <img src="../assets/img/medicne/bj-3.png" alt class="bj-3" />
            <img src="../assets/img/medicne/bj-4.png" alt class="bj-4" />

            <div style="display: flex;">
              <div style="width: 50%;">
                <div class="title">TOP5种类本月销量详情</div>
                <linegraph
                  class="allnav"
                  :id="'bargraph17'"
                  :data="productPie_option"
                  style="height:500px; width: 98%"
                ></linegraph>
              </div>
              <div style="width: 50%;">
                <div class="title" style="width: 100%;">各种类行业对比</div>
                <linegraph
                  class="allnav"
                  :id="'bargraph18'"
                  :data="planOption"
                  style="height:500px; width: 98%"
                ></linegraph>
              </div>
            </div>
          </div>
        </li>
      </ul>
    </div>

    <div class="back"></div>
    <div class="footer">豆管科技提供 www.doqtech.com.cn</div>
  </div>
</template>
<script>
import linegraph from "./linegraph";

import echarts from "echarts";

import html2canvas from "html2canvas";

export default {
  components: {
    linegraph
  },
  data() {
    return {
      month: "",
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
      ym_hot_kw: null,
      myColors: [
        "rgba(0,153,255,0.5)",
        "rgba(0,153,255,0.52)",
        "rgba(0,153,255,0.53)",
        "rgba(0,153,255,0.54)"
      ],
      date_X: null,

      /* 门店详情 */
      shopName: null,
      tuangou_mailiang: null,
      new_add_comment: null,
      avg_consume: null,
      start_rank: null,
      env_score: null,
      service_score: null,
      quality_score: null,

      /* 门店星级变化情况 */
      shopStar: null,
      /*门店人均消费金额变化情况 */
      shopAvgConsume: null,

      haoping_Y: null,
      xiaoguo_y: null,
      huangjing_Y: null,
      fuwu_Y: null,
      dijia_Y: null,
      gaojia_Y: null,

      shop3Score: null,
      showShopComment: null,
      /* 产品总销量排名 TOP10 */

      total_avg_price: null,
      productCountTopTen: null,
      /* 产品本月销量排名 TOP10*/
      current_avg_price: null,
      currentMonthProductTopTen: null,
      echart_product_type_shop: null,
      echart_product_type_shop_add: null,
      productPie_option: null,
      planOption: null,
      mapOption: null
    };
  },
  methods: {
    httpeshop() {
      var yimeiform = sessionStorage.getItem("sendYimeiform");
      yimeiform = JSON.parse(yimeiform);
      var shopId = yimeiform.shopId;
      var month = yimeiform.month;
      this.month = yimeiform.month;
      console.log(month + "test")
      month = month.replace("年", "-");
      month = month.replace("月", "");
    //   console.log(yimeiform);
      this.$axios
        // 医美
        .post(
          `http://bi.doqtech.com.cn/dianping/ym/find/shop/${shopId}/${month}.json`
        )
        .then(res => {
          console.log(res);
          //   店名
          this.shopName = res.data.data.shopName;
          var date_X = res.data.data.date_X;

          this.tuangou_mailiang = res.data.data.tuangou_mailiang;
          this.new_add_comment = res.data.data.new_add_comment;
          this.avg_consume = res.data.data.avg_consume;
          this.start_rank = res.data.data.start_rank;
          this.env_score = res.data.data.env_score;
          this.service_score = res.data.data.service_score;
          this.quality_score = res.data.data.quality_score;
          //门店星级变化情况

          var start_rank_Y = res.data.data.start_rank_Y;
          var shopStar = {
            tooltip: {
              trigger: "axis"
            },

            grid: {
              x: 46,
              y: 30,
              x2: 32,
              y2: 40,
              borderWidth: 0
            },
            calculable: true,
            xAxis: [
              {
                type: "category",
                boundaryGap: false,
                data: date_X,
                splitLine: {
                  show: false
                },
                axisLabel: {
                  show: true,
                  textStyle: {
                    color: "#a4a7ab"
                  }
                }
              }
            ],
            yAxis: [
              {
                type: "value",
                splitLine: {
                  show: false
                },
                axisLabel: {
                  show: true,
                  textStyle: {
                    color: "#a4a7ab"
                  }
                }
              }
            ],
            series: [
              {
                name: "门店星级",
                type: "line",

                smooth: true,

                lineStyle: {
                  color: "#E87C25"
                },
                itemStyle: {
                  normal: {
                    color: "#E87C25",
                    borderColor: "rgba(221, 220, 107, .1)",
                    borderWidth: 12
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
                          color: "rgba(1, 132, 213, 0.1)"
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
                data: start_rank_Y
              }
            ]
          };
          this.shopStar = shopStar;

          //门店人均消费金额变化情况
          var avg_consume_Y = res.data.data.avg_consume_Y;
          var shopAvgConsume = {
            tooltip: {
              trigger: "axis"
            },

            grid: {
              x: 46,
              y: 30,
              x2: 32,
              y2: 40,
              borderWidth: 0
            },
            calculable: true,
            xAxis: [
              {
                type: "category",
                boundaryGap: false,
                data: date_X,
                splitLine: {
                  show: false
                },
                axisLabel: {
                  show: true,
                  textStyle: {
                    color: "#a4a7ab"
                  }
                }
              }
            ],
            yAxis: [
              {
                type: "value",
                splitLine: {
                  show: false
                },
                axisLabel: {
                  show: true,
                  textStyle: {
                    color: "#a4a7ab"
                  }
                }
              }
            ],
            series: [
              {
                name: "人均消费金额",
                type: "line",
                smooth: true,
                lineStyle: {
                  color: "#B5C334"
                },
                itemStyle: {
                  normal: {
                    color: "#B5C334",
                    borderColor: "rgba(221, 220, 107, .1)",
                    borderWidth: 12
                  }
                },
                data: avg_consume_Y,
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
                          color: "rgba(1, 132, 213, 0.1)"
                        },
                        {
                          offset: 0.8,
                          color: "rgba(1, 132, 213, 0.1)"
                        }
                      ],
                      false),
                    shadowColor: "rgba(0, 0, 0, 0.1)"
                  }
                }
              }
            ]
          };
          this.shopAvgConsume = shopAvgConsume;

          this.haoping_Y = res.data.data.haoping_Y;
          this.xiaoguo_y = res.data.data.xiaoguo_y;
          this.huangjing_Y = res.data.data.huangjing_Y;
          this.fuwu_Y = res.data.data.fuwu_Y;
          this.dijia_Y = res.data.data.dijia_Y;
          this.gaojia_Y = res.data.data.gaojia_Y;

          //本月门店3分变化情况

          var env_score_Y = res.data.data.env_score_Y;
          var service_score_Y = res.data.data.service_score_Y;
          var quality_score_Y = res.data.data.quality_score_Y;
          var shop3Score = {
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
              data: ["效果分", "环境分", "服务分"]
            },
            grid: {
              x: 46,
              y: 30,
              x2: 32,
              y2: 40,
              borderWidth: 0
            },
            calculable: true,
            xAxis: [
              {
                type: "category",
                boundaryGap: false,
                data: date_X,
                splitLine: {
                  show: false
                },
                axisLabel: {
                  show: true,
                  textStyle: {
                    color: "#a4a7ab"
                  }
                }
              }
            ],
            yAxis: [
              {
                type: "value",
                splitLine: {
                  show: false
                },
                axisLabel: {
                  show: true,
                  textStyle: {
                    color: "#a4a7ab"
                  }
                }
              }
            ],
            series: [
              {
                name: "效果分",
                type: "line",
                smooth: true,
                data: quality_score_Y,
                lineStyle: {
                  color: "#B5C334"
                },
                itemStyle: {
                  normal: {
                    color: "#B5C334"
                  }
                }
              },
              {
                name: "环境分",
                type: "line",
                lineStyle: {
                  color: "#FCCE10"
                },
                smooth: true,
                data: env_score_Y,
                itemStyle: {
                  normal: {
                    color: "#FCCE10"
                  }
                }
              },
              {
                name: "服务分",
                type: "line",
                lineStyle: {
                  color: "#E87C25"
                },
                smooth: true,
                data: service_score_Y,
                itemStyle: {
                  normal: {
                    color: "#E87C25"
                  }
                }
              }
            ]
          };
          this.shop3Score = shop3Score;
          //   门店本月评论数走势图
          this.date_X = res.data.data.date_X;
          var start1_Y = res.data.data.start1_Y;
          var start2_Y = res.data.data.start2_Y;
          var start3_Y = res.data.data.start3_Y;
          var start4_Y = res.data.data.start4_Y;
          var start5_Y = res.data.data.start5_Y;

          var showShopComment = {
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
              data: ["5星", "4星", "3星", "2星", "1星"]
            },
            grid: {
              x: 46,
              y: 30,
              x2: 32,
              y2: 40,
              borderWidth: 0
            },
            calculable: true,
            xAxis: [
              {
                type: "category",
                boundaryGap: false,
                data: date_X,
                splitLine: {
                  show: false
                },
                axisLabel: {
                  show: true,
                  textStyle: {
                    color: "#a4a7ab"
                  }
                }
              }
            ],
            yAxis: [
              {
                type: "value",
                splitLine: {
                  show: false
                },
                axisLabel: {
                  show: true,
                  textStyle: {
                    color: "#a4a7ab"
                  }
                }
              }
            ],
            series: [
              {
                name: "5星",
                type: "line",
                smooth: true,
                data: start5_Y,
                lineStyle: {
                  color: "#C1232B"
                },
                itemStyle: {
                  normal: {
                    color: "#C1232B"
                  }
                }
              },
              {
                name: "4星",
                type: "line",
                smooth: true,
                data: start4_Y,
                lineStyle: {
                  color: "#B5C334"
                },
                itemStyle: {
                  normal: {
                    color: "#B5C334"
                  }
                }
              },
              {
                name: "3星",
                type: "line",
                smooth: true,
                data: start3_Y,
                lineStyle: {
                  color: "#FCCE10"
                },
                itemStyle: {
                  normal: {
                    color: "#FCCE10"
                  }
                }
              },
              {
                name: "2星",
                type: "line",
                smooth: true,
                data: start2_Y,
                lineStyle: {
                  color: "#E87C25"
                },
                itemStyle: {
                  normal: {
                    color: "#E87C25"
                  }
                }
              },
              {
                name: "1星",
                type: "line",
                smooth: true,
                data: start1_Y,
                lineStyle: {
                  color: "#27727B"
                },
                itemStyle: {
                  normal: {
                    color: "#27727B"
                  }
                }
              }
            ]
          };
          this.showShopComment = showShopComment;
          //   产品总销量排名 TOP10
          this.total_avg_price = res.data.data.total_avg_price;
          this.productCountTopTen = res.data.data.productCountTopTen;
          // 产品本月卖量榜 TOP10
          this.current_avg_price = res.data.data.current_avg_price;
          this.currentMonthProductTopTen =
            res.data.data.currentMonthProductTopTen;

          // 各种类销量排名榜
          var totalDataList_zhexian_X = res.data.data.totalDataList_zhexian_X;
          var totalDataList_zhexian_Y = res.data.data.totalDataList_zhexian_Y;
          var totalDataList_bingtu = res.data.data.totalDataList_bingtu;

          var echart_product_type_shop = {
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
                  left: "60%",
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
                textStyle: {
                  color: "#9ea7c4",
                  fontSize: 14
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
                  fontSize: 14
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
                    shadowBlur: 20,
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
                      fontSize: 14
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
                    shadowBlur: 20,
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
          this.echart_product_type_shop = echart_product_type_shop;
          //各种类本月卖量排名榜
          var monthDataList_zhexian_X = res.data.data.monthDataList_zhexian_X;
          var monthDataList_zhexian_Y = res.data.data.monthDataList_zhexian_Y;
          var monthDataList_bingtu = res.data.data.monthDataList_bingtu;

          var echart_product_type_shop_add = {
            graphic: {
              elements: [
                {
                  type: "image",
                  style: {
                    image:
                      "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEAAAABACAMAAACdt4HsAAAAA3NCSVQICAjb4U/gAAAACXBIWXMAAAHCAAABwgHoPH1UAAAAGXRFWHRTb2Z0d2FyZQB3d3cuaW5rc2NhcGUub3Jnm+48GgAAAtlQTFRF////////////////4+Pj9PT04lhO41VM7u7u21RI62RY62JW7GFZ6mJX7u7u6mBa62NY7u7u62FX62NZ62JY7+/v7GFX7u7u3JWQ1FJH7+/v7+/v8PDw8PDw7+/v0oiD4ldN7+/v7tbV7+/v79nW8PDw8PDw7+/v7+/v21RJ62JY7+/v62JZ62NY7Ghd7+/v7Gpf62JY62JY62JY62JY7+/v62JY62JY7u7u7+/v7+/v7b263Lq30lFG7s7L7+/v7+/v7+/v4ldM0bOx7+/v7+/vu0g+vEg+vUk/vkk/v0k/v0o/xEtBxExBxUtCxUxBxktCxkxCx0xDx01CyExDyE1CyE1DyU1DyU5Dyk1Eyk5Dy01Ey05EzE5EzU5Fzk9Ezk9Fz09Fz1BF0E9F0FBF0FBG0VBG0VFG0dHR01FH1FFH1VFH1VJH1VJI1lJH2VNI2VNJ2dnZ2lNJ2lRJ2tra21RJ21RK3FRK3FVK3Nzc3VVK31ZL4FZL4VZM4VdM4eHh4ldM4ldN4lhN41hN41lO5FlO5FlP5FpP5lxR5lxS511S6F5U6F9U6F9V6Ojo6V9V6enp6mFX6urq62FX62JY62NZ62Ra62Vb62Vc62Zc62dd62he62lf62lg62pg62th621k625k625l63Bn63Fo7HRs7HVt7Hdv7Hpx7Hpy7H107H117H527H937IF57IV97IZ/7IeA7IiB7IqD7IyF7I6H7I+I7JCJ7JGK7JOM7JON7JaQ7ZiR7ZqU7ZyW7Z2X7aCa7aSe7aSf7aWg7aah7amk7aum7ayn7a2o7bGt7bKt7bSw7bq27rq37r267r+87sC97sG+7sPA7sXC7snG7snH7svI7s7M7s/N7tHP7tbU7tfW7tjW7tjX7tzb7t3b797d79/e7+Df7+Hg7+Lh7+Pj7+bm7+fn7+jn7+jo7+no7+np7+rp7+rq7+vr7+zr7+3t7+7u7+/vaynTPwAAAEZ0Uk5TAAMFBwkXGhseQEBBQklJSktLTE1OTk9ZZXBzfYWGkpSWnqmrsLW2vL3AwMDBwsXFxsnKy8zMzc7Y3+Tp6+/v7/Dy+Pv9/rEt8ycAAAPWSURBVFjD7ZbnX9NAGMfj3nvvvXDvvbU4o4KKAwd6anErRhlVDxAFcVUjuPdGXLgRF+69N04QVxn9C7y7JM0lbUNa3/q8aJPnft9v0stdP2EYzSrs4VGYcb+KNOFRNSniElS8VvNODauVy8cwRZvyYjUtyjAFK1Rv26Nx1VK5tPGCDaxC9andjKeqRd2+4kCd3Fp8nrZWW6XEy/zxj3K/fl4NQRUrVVlXJP5aNt2vrCFoTAet2YkCn6ToWutpCHqSxIMDh2/8JPdwBvPnyPXTkw8deECGu2sIOpLEPkTFp+GjjDiej8vAR6lHUHMfGe7gnC/WjSTInR8j130XG/uO3MtR3Eskw52LOcFLtOQTSOLXcZy+T45v3iRfd8mz+IUPf+/lW5ZwgJdshTOvSNxyZw/P7/hKLp2FP79s4/k9dyykcR7nWpVU4aVbCxO+84Mw05Yn1xMuyxN/OeH6E4swcEF8tK1LU3iZNrYls/uxVaveHJRXV5syIl62Hb1o+dPPM5zQPx6e2qiItiuL8PLteXVtv/j0tx2d+ez8Frsk3748s2KtfZvffsuiFvy5vdNBcO0KBsLlq1XdzVfTHP2C78lbVcHVyyFEAggjVlHdmEufnU1h6pVNVHBVBGaJACmipfbZFAXz+rXi9FOiNI3REQIpCiBcRhQn3iryKWg3nVEa35MNFr1M4mwCrIh/qch+S4ohvynpm6L99qSMKwQQzltD5dLlOduanE4NrF9KMwqB0WhTZN7bRc/3rruZNjwoSENgNC5Yh/+LHu1XP/H9j7JFPAcBVryIc7Bm+LgXAq4S1OylFhiN4Ss32PMbVoYHBakFvWoyTIFpS9QCCMOjzErcHBUOoVqwZFZ+vBsNA6aa1AIIw2iFOSoM95SCxTOGs2Q7D/I09AcmtQDC0EhRYY4MFTq0wDTdix3qRwRgAlZMMqkFqLDCHGk7lQUmf4zP4QQBABMGexr6TQyxEyBFJHUiCUL8h7HDJs/lOJsAKYYghQOBoiTBUNZrynyOUwgA8BviqVfgNTWA4+wEAEzSK5BwtQDoFXA5CXyDHeHBfroFBs8xdorAiSyrW+Dd32DwCaTxRQj38dctAGAEUoxcKOELxyN8Ose5IBAVHMYDxrHs6Bk47pIAAB+k8A4I8EX4TCHuogApBhgMLDt2thR3WQDAqIG+s+W4GwIAOO6/QIegUld3BY0KiW9JksI1gQ2XFa4IFLik0C+wwwWFXoFDHFeN3noEXSpqvO8LCi2BJi4pnAtyxAWFM4EuXLm0aIHTqdNWuIXTCjdxWeE2Lin+ARcUOeF/AdDEkV5yNqXkAAAAAElFTkSuQmCC",
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
                textStyle: {
                  color: "#9ea7c4",
                  fontSize: 14
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
                  fontSize: 14
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
                    shadowBlur: 20,
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
                      fontSize: 14
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
                    shadowBlur: 30,
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
          this.echart_product_type_shop_add = echart_product_type_shop_add;
          //    TOP5种类本月销量详情
          var productClassColor = [
            "rgba(255,153,0,",
            "rgba(153,204,102,",
            "rgba(0,102,255,",
            "rgba(80,102,255,",
            "rgba(153,24,30,"
          ];

          var top_inner_listold = res.data.data.top_inner_list;

          var top_inner_list = new Array();
          for (let i = 0; i < top_inner_listold.length; i++) {
            var innerObj = new Object();
            var numarr = ["①", "②", "③", "④", "⑤", "⑥", "⑦", "⑧", "⑨", "⑩"];
            let name = numarr[i] + top_inner_listold[i].name;
            let value = top_inner_listold[i].value;
            innerObj.name = name;
            innerObj.value = value;
            top_inner_list.push(innerObj);
          }
          var top_outer_list = res.data.data.top_outer_list;

          var productData = [];
          var productColor = [];
          for (var i = 0; i < top_inner_listold.length; i++) {
            var total = 0;
            for (var j = 0; j < top_outer_list[i].length; j++) {
              var n = Math.round(Math.random() * 100) + 1;
              productData.push({ name: top_outer_list[i][j], value: n });
              total += n;
            }
            for (var j = 0; j < top_outer_list[i].length; j++) {
              productColor.push(
                productClassColor[i] +
                  (1.0 - productData[j].value / total).toFixed(2) +
                  ")"
              );
            }
          }

          var productPie_option = {
            title: {
              text: "销售额",
              x: "center",
              y: "center",
              itemGap: 10,
              textStyle: {
                color: "#09F",
                fontWeight: "normal",
                fontFamily: "微软雅黑",
                fontSize: "12"
              }
            },
            calculable: false,
            tooltip: {
              trigger: "item",
              textStyle: {
                color: "#FFF",
                fontSize: "12"
              },
              formatter: "{a} <br/>{b} : {c} ({d}%)"
            },
            series: [
              {
                name: "类别",
                type: "pie",
                selectedMode: "single",
                radius: ["20%", "40%"],
                width: "40%",
                funnelAlign: "right",
                itemStyle: {
                  normal: {
                    color: function(d) {
                      return productClassColor[d.dataIndex] + "1)";
                    },
                    borderColor: "#032749",
                    label: {
                      position: "inner",
                      fontSize: 14
                    },
                    labelLine: {
                      show: true
                    }
                  }
                },
                data: top_inner_list
              },
              {
                name: "商品",
                type: "pie",
                radius: ["40%", "70%"],
                width: "35%",
                funnelAlign: "left",
                itemStyle: {
                  normal: {
                    // color: function(d) {
                    //   return productColor[d.dataIndex];
                    // },
                    borderColor: "#032749",
                    label: {
                      color: "#B7E1FF",
                      fontSize: "12"
                    }
                  }
                },
                data: top_outer_list
              }
            ]
          };
          this.productPie_option = productPie_option;
          //各种类行业对比

          var industryContrast_X = res.data.data.industryContrast_X;
          var bendian_Y = res.data.data.bendian_Y;
          var diqu_Y = res.data.data.diqu_Y;
          var color = ["#F35331", "#2499F8", "#3DF098", "#33B734"];

          var planOption = {
            color:["#c23531","#FF9900"],
            tooltip: {
              trigger: 'axis',
              axisPointer: {
                crossStyle: {
                  color: '#999'
                }
              }
            },
            legend: {
              data:['本店销量','地区销量'],
              textStyle:{//图例文字的样式
                color: "rgba(255,255,255,.6)",
                fontSize: "16"
              }
            },
            xAxis: [
              {
                type: 'category',
                data: industryContrast_X,
                axisPointer: {
                  type: 'shadow'
                },
                axisLabel: {
                  textStyle: {
                    color: "rgba(255,255,255,.6)",
                    fontSize: "16"
                  }
                }
              }
            ],
            yAxis: [
              {
                type: 'value',
                name: '本店销量',
                nameTextStyle:{
                  color: "rgba(255,255,255,.6)",
                  fontSize: "16"
                },
                axisTick: {
                  show: false
                },
                axisLabel: {
                  textStyle: {
                    color: "rgba(255,255,255,.6)",
                    fontSize: "16"
                  }
                },
                splitLine:{
                  show:false
                }
              },
              {
                type: 'value',
                name: '地区销量',
                nameTextStyle:{
                  color: "rgba(255,255,255,.6)",
                  fontSize: "16"
                },
                axisTick: {
                  show: false
                },
                axisLabel: {
                  textStyle: {
                    color: "rgba(255,255,255,.6)",
                    fontSize: "16"
                  }
                },
                splitLine:{
                  show:false
                }
              }
            ],
            series: [
              {
                name:'本店销量',
                type:'bar',
                data:bendian_Y,
                itemStyle : { normal: {label : {show: true}}}
              },
              {
                name:'地区销量',
                type:'line',
                yAxisIndex: 1,
                data:diqu_Y,
                itemStyle : { normal: {label : {show: true}}}
              }
            ]
        };
          this.planOption = planOption;
        })
        .catch(err => {
          console.log(err);
        });
    }
  },
  created() {
    this.httpeshop();
  }
};
</script>