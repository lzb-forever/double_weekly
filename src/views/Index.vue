<template>
  <div>
    <div class="el-center">
      <div>
        <div class="text">选择日期：</div>
        <el-form :inline="true" :model="yimeiform" class="demo-form-inline flex">
          <el-form-item>
            <el-date-picker v-model="yimeiform.month" align="right" type="month"  value-format="yyyy年MM月" placeholder="选择月"></el-date-picker>
          </el-form-item>

          <div class="text">选择商户：</div>
          <el-form-item>
            <el-select v-model="yimeiform.accountId" placeholder="商户">
              <el-option label="花下" value="CsOs45SAIVVREp3hzbVVN7uvgv2ASPfw"></el-option>
            </el-select>
          </el-form-item>
          <div class="text">选择门店：</div>
          <el-form-item>
            <el-select v-model="yimeiform.shopId" placeholder="门店">
              <el-option label="丽诗丽格·眼综合整形店" value="4192157"></el-option>
              <el-option label="芙艾医美" value="63181023"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="onyimei">医美报表</el-button>
          </el-form-item>
        </el-form>
      </div>
    </div>
  </div>
</template>

<script>
import "../assets/style/style.css";
export default {
  data() {
    return {
      accountId: [
        {
          value: "CsOs45SAIVVREp3hzbVVN7uvgv2ASPfw",
          name: "花下",
          enterDate: "2019-4-16"
        },
        {
          value: "r2miTSS5BsaaVrKgusphwbx2vp7xHX1z",
          name: "ritz",
          enterDate: "2019-6-11"
        },
        {
          value: "pb0FXqgfdDMDxo6lh3MVU1cqhKRWUW7g",
          name: "欣妍抗衰中心",
          enterDate: "2019-8-29"
        },
        {
          value: "6AWt6YcnQB7s9TgC3dyNuQ1R9DIqGuQd",
          name: "I Miss U美甲美睫",
          enterDate: "2019-09-02"
        },
        {
          value: "jg4LunoO6ALCu2Dv30Q94cnpIqjZY9pq",
          name: "IVO健身",
          enterDate: "2019-09-02"
        },
        {
          value: "6paUXDK8WWmUqSio55JdlQY2CfuZkgrQ",
          name: "Project X健身",
          enterDate: "2019-6-14"
        },
        {
          value: "TWR2sGlFWn5umGwhwpRn9psjmq43uCxP",
          name: "ERAfitness",
          enterDate: "2019-09-02"
        },
        {
          value: "uM29mOtrB05VoCCshUzKpHx0iRcERUAF",
          name: "齐脉养生",
          enterDate: "2019-09-02"
        },
        {
          value: "TFhUvJd2zXLed9tH86Fb8urjW8vY9RWn",
          name: "super coach",
          enterDate: "2019-9-16"
        },
        {
          value: "I4flqj8Bq2Qe436UoF6PiXvtj9dfkDol",
          name: "yu+fit",
          enterDate: "2019-9-12"
        },
        {
          value: "lIJxNgrNjhdpLcSnq0G23gJx4tD2Qb0j",
          name: "艾医灸舍",
          enterDate: "2019-8-26"
        },
        {
          value: "oaIwTQGDQ9sunto80lhaqjNiKpvp9Baj",
          name: "柏丽美",
          enterDate: "2019-8-30"
        },
        {
          value: "FvfzZ4nQpvPbMCS4AFs29xVa3crl0ZVR",
          name: "吉瘦",
          enterDate: "2019-5-22"
        },
        {
          value: "HgyDZraL2b93MLRpbw0SboxhLZSS6JQq",
          name: "东英经典",
          enterDate: "2019-9-21"
        }
      ],
      yimeiform: {
        month: "",
        accountId:"",
        shopId: "",
      }
    };
  },
  methods: {
    onyimei() {
      var yimeiform = this.yimeiform
      console.log(yimeiform)
      sessionStorage.setItem("sendYimeiform",JSON.stringify(yimeiform))

      this.$router.push({
        path: "/medicine"
      });
    }
  }
};
</script>

<style scoped>
.el-center {
  display: flex;
  justify-content: center;
  margin-top: 100px;
}
.flex {
  display: flex;
  flex-direction: row;
}
.text {
  font-size: 16px;
  font-weight: 400;
  color: #fff;
  line-height: 40px;
  margin-left: 20px;
}
.el-form-item {
  margin-bottom: 0;
}
</style>