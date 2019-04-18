<template>
  <div class="pos">
    <el-row>
      <el-col :span="7" class="pos-order" id="order-list">
        <el-tabs @tab-click="orderTabClick">
          <el-tab-pane label="点餐">
            <el-table :data="tableData" border style="width: 100%">
              <el-table-column prop="goodsName" label="商品"></el-table-column>
              <el-table-column prop="price" label="单价" width="70"></el-table-column>
              <el-table-column prop="count" label="数量" width="70"></el-table-column>
              <el-table-column label="操作" width="120" fixed="right">
                <template scope="scope">
                  <el-button type="text" size="medium" @click="delOneGoods(scope.row)">删除</el-button>
                  <el-button type="text" size="medium" @click="addOrderList(scope.row)">增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="total">
              <span class="count">总数量：{{totalCount}}</span>
              <span>总金额：{{totalMoney}}元</span>
            </div>
            <div class="btn-group">
              <el-button type="warning">挂单</el-button>
              <el-button type="danger" @click="delAllGoods">删除</el-button>
              <el-button type="success" @click="checkout">结账</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label="挂单">挂单</el-tab-pane>
          <el-tab-pane label="外卖">外卖</el-tab-pane>
        </el-tabs>
      </el-col>

      <el-col :span="17">
        <div class="often-goods">
          <div class="o-goods-title">常用商品</div>
          <div class="o-goods-list">
            <ul>
              <li v-for="item in oftenGoods" :key="item.goodsId" @click="addOrderList(item)">
                <span>{{item.goodsName}}</span>
                <span class="o-goods-price">￥{{item.price}}元</span>
              </li>
            </ul>
          </div>
        </div>

        <div class="goods-type">
          <el-tabs @tab-click="goodsTabClick">
            <el-tab-pane label="汉堡">
              <div class="hanbao-pane">
                <ul>
                  <li v-for="item in type0Goods" :key="item.goodsId" @click="addOrderList(item)">
                    <img class="food-img" :src="'https://tuimeizi.cn/random?w=60&h=60' || item.goodsImg">
                    <div class="food-text">
                      <span class="food-name">{{item.goodsName}}</span>
                      <br>
                      <span class="food-price">￥{{item.price}}元</span>
                    </div>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="小食">
              <div class="hanbao-pane">
                <ul>
                  <li v-for="item in type1Goods" :key="item.goodsId" @click="addOrderList(item)">
                    <img class="food-img" :src="'https://tuimeizi.cn/coser?w=60&h=60' || item.goodsImg">
                    <div class="food-text">
                      <span class="food-name">{{item.goodsName}}</span>
                      <br>
                      <span class="food-price">￥{{item.price}}元</span>
                    </div>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="饮料">
              <div class="hanbao-pane">
                <ul>
                  <li v-for="item in type2Goods" :key="item.goodsId" @click="addOrderList(item)">
                    <img class="food-img" :src="'https://tuimeizi.cn/logo?w=60&h=60' || item.goodsImg">
                    <div class="food-text">
                      <span class="food-name">{{item.goodsName}}</span>
                      <br>
                      <span class="food-price">￥{{item.price}}元</span>
                    </div>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="套餐">
              <div class="hanbao-pane">
                <ul>
                  <li v-for="item in type3Goods" :key="item.goodsId" @click="addOrderList(item)">
                    <img class="food-img" :src="'https://tuimeizi.cn/sexy?w=60&h=60' || item.goodsImg">
                    <div class="food-text">
                      <span class="food-name">{{item.goodsName}}</span>
                      <br>
                      <span class="food-price">￥{{item.price}}元</span>
                    </div>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
          </el-tabs>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "Pos",
  data() {
    return {
      tableData: [],
      oftenGoods: [],
      type0Goods: [],
      type1Goods: [],
      type2Goods: [],
      type3Goods: [],
      totalCount: 0,
      totalMoney: 0,
      
      // tableData: [
      //   {
      //     goodsName: "可口可乐",
      //     price: 8,
      //     count: 1
      //   },
      //   {
      //     goodsName: "香辣鸡腿堡",
      //     price: 15,
      //     count: 1
      //   },
      //   {
      //     goodsName: "爱心薯条",
      //     price: 8,
      //     count: 1
      //   },
      //   {
      //     goodsName: "甜筒",
      //     price: 8,
      //     count: 1
      //   }
      // ],
      // oftenGoods: [
      //   {
      //     goodsId: 1,
      //     goodsName: "香辣鸡腿堡",
      //     price: 18
      //   },
      //   {
      //     goodsId: 2,
      //     goodsName: "田园鸡腿堡",
      //     price: 15
      //   },
      //   {
      //     goodsId: 3,
      //     goodsName: "和风汉堡",
      //     price: 15
      //   },
      //   {
      //     goodsId: 4,
      //     goodsName: "快乐全家桶",
      //     price: 80
      //   },
      //   {
      //     goodsId: 5,
      //     goodsName: "脆皮炸鸡腿",
      //     price: 10
      //   },
      //   {
      //     goodsId: 6,
      //     goodsName: "魔法鸡块",
      //     price: 20
      //   },
      //   {
      //     goodsId: 7,
      //     goodsName: "可乐大杯",
      //     price: 10
      //   },
      //   {
      //     goodsId: 8,
      //     goodsName: "雪顶咖啡",
      //     price: 18
      //   },
      //   {
      //     goodsId: 9,
      //     goodsName: "大块鸡米花",
      //     price: 15
      //   },
      //   {
      //     goodsId: 20,
      //     goodsName: "香脆鸡柳",
      //     price: 17
      //   }
      // ],
      // type0Goods: [
      //   {
      //     goodsId: 1,
      //     goodsImg: "https://tuimeizi.cn/random?w=60&h=60",
      //     goodsName: "香辣鸡腿堡",
      //     price: 18
      //   },
      //   {
      //     goodsId: 2,
      //     goodsImg: "https://tuimeizi.cn/coser?w=60&h=60",
      //     goodsName: "田园鸡腿堡",
      //     price: 15
      //   },
      //   {
      //     goodsId: 3,
      //     goodsImg: "https://tuimeizi.cn/pure?w=60&h=60",
      //     goodsName: "和风汉堡",
      //     price: 15
      //   },
      //   {
      //     goodsId: 4,
      //     goodsImg: "https://tuimeizi.cn/sexy?w=60&h=60",
      //     goodsName: "快乐全家桶",
      //     price: 80
      //   },
      //   {
      //     goodsId: 5,
      //     goodsImg: "https://tuimeizi.cn/games?w=60&h=60",
      //     goodsName: "脆皮炸鸡腿",
      //     price: 10
      //   },
      //   {
      //     goodsId: 6,
      //     goodsImg: "https://tuimeizi.cn/logo?w=60&h=60",
      //     goodsName: "魔法鸡块",
      //     price: 20
      //   },
      //   {
      //     goodsId: 7,
      //     goodsImg: "https://tuimeizi.cn/pure?w=60&h=60",
      //     goodsName: "可乐大杯",
      //     price: 10
      //   },
      //   {
      //     goodsId: 8,
      //     goodsImg: "https://tuimeizi.cn/coser?w=60&h=60",
      //     goodsName: "雪顶咖啡",
      //     price: 18
      //   },
      //   {
      //     goodsId: 9,
      //     goodsImg: "https://tuimeizi.cn/logo?w=60&h=60",
      //     goodsName: "大块鸡米花",
      //     price: 15
      //   },
      //   {
      //     goodsId: 20,
      //     goodsImg: "https://tuimeizi.cn/pure?w=60&h=60",
      //     goodsName: "香脆鸡柳",
      //     price: 17
      //   }
      // ]
    };
  },
  created() {
    /**
     * 请求常用商品数据
     */
    axios.get('https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods')
    .then(res => {
      console.log(res);
      
      this.oftenGoods = res.data;
    })
    .catch(err => {
      console.log(err);
      alert('网络错误，暂不可访问');
    });

    /**
     * 请求分类商品数据
     */
    axios.get('https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/typeGoods')
    .then(res => {
      console.log(res);
      
      this.type0Goods = res.data[0];
      this.type1Goods = res.data[1];
      this.type2Goods = res.data[2];
      this.type3Goods = res.data[3];
    })
    .catch(err => {
      console.log(err);
      alert('网络错误，暂不可访问');
    });
  },
  mounted() {
    let orderHeight = document.body.clientHeight;
    document.getElementById("order-list").style.height = orderHeight + "px";
  },
  methods: {
    /**
     * 增加商品
     * goods: 当前需增加的商品对象
     */
    addOrderList(goods){
      // 1、判断原订单列表是否有该商品
      let isHasGoods = false;
      for(let i=0; i<this.tableData.length; i++){
        if (this.tableData[i].goodsId == goods.goodsId) {
          isHasGoods = true;
        }
      }

      // 2、根据(1)的值处理业务逻辑: 整列增加 / 原商品数量增加
      if (isHasGoods) {
        // 已经有该商品 原商品数量增加
        let arr = this.tableData.filter(item => item.goodsId == goods.goodsId);
        arr[0].count++;
      } else {
        // 新追加商品 整列增加
        let newGoods = {count: 1, ...goods};
        this.tableData.push(newGoods);
      }

      // 计算汇总 总数量、总金额
      this.countMoney();
    },

    /**
     * 删除单个商品
     */
    delOneGoods(goods) {
      this.tableData = this.tableData.filter(item => item.goodsId != goods.goodsId);
      this.countMoney();
    },

    /**
     * 删除所有商品
     */
    delAllGoods() {
      if (this.totalCount>0) {
        this.$confirm('确定要删除该订单下的所有商品吗?', '温馨提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning',
          center: true
        }).then(() => {
          this.totalCount = 0;
          this.totalMoney = 0;
          this.tableData = [];
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });
        });
      } else {
        this.$message.error('暂未添加商品，无法进行删除操作！');
      }
    },

    /**
     * 模拟结账操作
     */
    checkout(){
      if (this.totalCount>0) { // 有商品，可结账
        // 清空商品列表，进行成功提示
        this.totalCount = 0;
        this.totalMoney = 0;
        this.tableData = [];
        this.$message.success('结账成功，感谢光临！');
      } else { // 无商品，不可结账
        // 进行相应提示
        this.$message({
          type: 'info',
          message: '暂无商品，无需结账！'
        });
      }
    },

    /**
     * 计算汇总 总数量、总金额， 计算前先 数据清零
     */
    countMoney() {
      this.totalCount = 0;
      this.totalMoney = 0;
      if (this.tableData) {
        this.tableData.forEach(item => {
          this.totalCount += item.count;
          this.totalMoney = this.totalMoney + (item.price * item.count);
        });
      }
    },

    /**
     * 订单标签页切换
     */
    orderTabClick: function(e) {
      this.updateTabsStyle(e, 0);
    },

    /**
     * 商品标签页切换
     */
    goodsTabClick: function(e) {
      this.updateTabsStyle(e, 1);
    },

    /**
     * 处理 tabs当前点击项样式问题
     * e: 事件对象
     * tabIndex: tabs组件索引
     */
    updateTabsStyle: function(e, tabIndex) {
      // DOM元素追加事件的特殊处理: this.$nextTick(callback);
      this.$nextTick(function() {
        if (e.index != 0) {
          let transX = parseInt(
            document
              .getElementsByClassName("el-tabs__active-bar")
              [tabIndex].style.transform.split("(")[1]
          );
          document.getElementsByClassName("el-tabs__active-bar")[
            tabIndex
          ].style.transform = "translateX(" + (transX - 20) + "px)";
        }
      });
    }
  }
};
</script>

<style scoped>
.pos {
  float: left;
  width: 94%;
}
.pos-order {
  background-color: #f9fafc;
  border-right: 1px solid #c0ccda;
}
.total {
  height: 60px;
  line-height: 60px;
  text-align: center;
  border-bottom: 1px solid #e5e9f2;
}
.total .count {
  margin-right: 20px;
}
.btn-group {
  margin-top: 15px;
}

.o-goods-title {
  height: 18px;
  line-height: 20px;
  text-align: left;
  padding: 10px;
  padding-left: 15px;
  border-bottom: 2px solid #e4e7ed;
  background-color: #f9fafc;
}

/* 清除浮动 两种方式 */
.o-goods-list ul {
  overflow: hidden;
}
/* .o-goods-list ul::after {
  content: '';
  display: block;
  clear: both;
} */

.o-goods-list ul li,
.hanbao-pane ul li {
  list-style: none;
  float: left;
  border: 1px solid #e5e9f2;
  border-radius: 4px;
  background-color: #fff;
  margin: 10px;
  padding: 10px;
  cursor: pointer;
}
.o-goods-price {
  color: #58b7ff;
}

.goods-type {
  clear: both;
  border-top: 2px solid #e4e7ed;
}
.hanbao-pane ul li {
  border-radius: 2px;
  padding: 2px 12px 2px 2px;
}
.food-img {
  float: left;
  margin-right: 10px;
}
.food-text {
  display: inline-block;
  margin-top: 8px;
}
.food-name {
  color: #ff0630;
}
</style>
