<template>
  <div class="sales-board">
      <div class="sales-board-intro">
        <h2>流量分析</h2>
        <p>贞丰糯米饭是一种早在清朝嘉庆年间已是颇有名气的地方风味小吃。主要原料系上等糯米，精选瘦肉。上碗时，切肉成薄片盖糯米饭上食用。贞丰油糯米饭制作工艺大致是：选取本地优质精糯米，先簸干扬净，用清水浸泡数小时，淘洗滤干后蒸熟，然后将冷却的糯米饭放入按适当比例配好的熟猪油锅内炒好备用，出售时，用铁锅装糯米饭，文火加温保热，配上鸡腿、红烧肉、香肠、特制的胡辣椒面、酸菜、折耳根等,即可食用。</p>
      </div>
      <div class="sales-board-form">
          <div class="sales-board-line">
              <div class="sales-board-line-left">
                  购买数量：
              </div>
              <div class="sales-board-line-right">
                <v-counter @on-change="onParamChange('buyNum', $event)"></v-counter>
              </div>
          </div>
          <div class="sales-board-line">
              <div class="sales-board-line-left">
                  产品类型：
              </div>
              <div class="sales-board-line-right">
                  <v-selection :selections="buyTypes" @on-change="onParamChange('buyType', $event)"></v-selection>
              </div>
          </div>
          <div class="sales-board-line">
              <div class="sales-board-line-left">
                  有效时间：
              </div>
              <div class="sales-board-line-right">
                  <v-chooser
                  :selections="periodList"
                  @on-change="onParamChange('period', $event)"></v-chooser>
              </div>
          </div>
          <div class="sales-board-line">
              <div class="sales-board-line-left">
                  产品版本：
              </div>
              <div class="sales-board-line-right">
                  <v-mul-chooser
                  :selections="versionList"
                  @on-change="onParamChange('versions', $event)"></v-mul-chooser>
              </div>
          </div>
          <div class="sales-board-line">
              <div class="sales-board-line-left">
                  总价：
              </div>
              <div class="sales-board-line-right">
                  {{ price }} 元
              </div>
          </div>
          <div class="sales-board-line">
              <div class="sales-board-line-left">&nbsp;</div>
              <div class="sales-board-line-right">
                  <div class="button" @click="showPayDialog">
                    立即购买
                  </div>
              </div>
          </div>
      </div>
      <div class="sales-board-des">
        <h2>产品说明</h2>
        <p>2001年注册的，牌子就叫‘胖四娘’”，快言快语的她自豪地告诉笔者。她母亲站在一旁说，胖四娘真名叫陆朝英，由于长相稍胖，在家又排行老四，人称胖四娘，加之从事油糯米饭经营20多年来，为人正直，热情好客，生意较其他家要好些，真正的名字没有几个人知道。2001年，以“胖四娘”为品牌注册了商标。临走时，胖四娘递给笔者一张名片，上面写着：“胖四娘特色油糯米饭”，还有联系电话和家庭住址。</p>

        <h3>特产做法</h3>
        <ul>
          <li>1.用冷水浸泡糯米8－9小时。</li>
          <li>2.将浸泡好的糯米用木蒸子或锅蒸熟，注意中途不要洒水，中间要经常用筷子把糯米扒散，使其蒸得软硬均匀。</li>
          <li>3.蒸熟后把糯米饭倒入盆内。</li>
          <li>4.用猪骨头加少量鸡精和盐巴熬汤（如没有猪骨头，可用猪油加少量水、鸡精和盐巴熬汤；一般十斤糯米饭，要半斤左右猪油）。</li>
          <li>5.好的油汤浇在糯米饭上，用筷子拌匀（注意汤不能太多，能将糯米饭搅拌散开即可）。</li>
        </ul>

        <h3>瘦肉片的做法</h3>
        <ul>
          <li>1.精选猪瘦肉。</li>
          <li>2.用八角、回香、花椒、桂皮、盐、酱油做成的香料腌渍四至五天，拿出瘦肉去掉香料。</li>
          <li>3.将菜油倒入铁锅内烧至六成热，下瘦肉块炸至半干。</li>
          <li>4.滤油晾冷后，切成薄片盖在糯米饭上食用。</li>
          <li>5.蒸好的糯米饭猪瘦肉炒好，装入铁锅内用文火保温待用</li>
        </ul>
      </div>
      <my-dialog :is-show="isShowPayDialog" @on-close="hidePayDialog">
        <table class="buy-dialog-table">
          <tr>
            <th>购买数量</th>
            <th>产品类型</th>
            <th>有效时间</th>
            <th>产品版本</th>
            <th>总价</th>
          </tr>
          <tr>
            <td>{{ buyNum }}</td>
            <td>{{ buyType.label }}</td>
            <td>{{ period.label }}</td>
            <td>
              <span v-for="item in versions">{{ item.label }}</span>
            </td>
            <td>{{ price }}</td>
          </tr>
        </table>
        <h3 class="buy-dialog-title">请选择银行</h3>
        <bank-chooser @on-change="onChangeBanks"></bank-chooser>
        <div class="button buy-dialog-btn" @click="confirmBuy">
          确认购买
        </div>
      </my-dialog>
      <my-dialog :is-show="isShowErrDialog" @on-close="hideErrDialog">
        支付失败！
      </my-dialog>
      <check-order :is-show-check-dialog="isShowCheckOrder" :order-id="orderId" @on-close-check-dialog="hideCheckOrder"></check-order>
  </div>
</template>

<script>
import VSelection from '../../components/base/selection'
import VCounter from '../../components/base/counter'
import VChooser from '../../components/base/chooser'
import VMulChooser from '../../components/base/multiplyChooser'
import Dialog from '../../components/base/dialog'
import BankChooser from '../../components/bankChooser'
import CheckOrder from '../../components/checkOrder'
import _ from 'lodash'
export default {
  components: {
    VSelection,
    VCounter,
    VChooser,
    VMulChooser,
    MyDialog: Dialog,
    BankChooser,
    CheckOrder
  },
  data () {
    return {
      buyNum: 0,
      buyType: {},
      versions: [],
      period: {},
      price: 0,
      versionList: [
        {
          label: '加腊肉',
          value: 0
        },
        {
          label: '加热狗',
          value: 1
        },
        {
          label: '加排骨',
          value: 2
        },
        {
          label: '尊享',
          value: 3
        }
      ],
      periodList: [
        {
          label: '一天',
          value: 0
        },
        {
          label: '两天',
          value: 1
        },
        {
          label: '一个星期',
          value: 2
        }
      ],
      buyTypes: [
        {
          label: '李记',
          value: 0
        },
        {
          label: '贺记',
          value: 1
        },
        {
          label: '熊记',
          value: 2
        },
        {
          label: '特级',
          value: 3
        }
      ],
      isShowPayDialog: false,
      bankId: null,
      orderId: null,
      isShowCheckOrder: false,
      isShowErrDialog: false
    }
  },
  methods: {
    onParamChange (attr, val) {
      this[attr] = val
      this.getPrice()
    },
    getPrice () {
      let buyVersionsArray = _.map(this.versions, (item) => {
        return item.value
      })
      let reqParams = {
        buyNumber: this.buyNum,
        buyType: this.buyType.value,
        period: this.period.value,
        version: buyVersionsArray.join(',')
      }
      this.$http.post('/api/getPrice', reqParams)
      .then((res) => {
        this.price = res.data.amount
      })
    },
    showPayDialog () {
      this.isShowPayDialog = true
    },
    hidePayDialog () {
      this.isShowPayDialog = false
    },
    hideErrDialog () {
      this.isShowErrDialog = false
    },
    hideCheckOrder () {
      this.isShowCheckOrder = false
    },
    onChangeBanks (bankObj) {
      this.bankId = bankObj.id
    },
    confirmBuy () {
      let buyVersionsArray = _.map(this.versions, (item) => {
        return item.value
      })
      let reqParams = {
        buyNumber: this.buyNum,
        buyType: this.buyType.value,
        period: this.period.value,
        version: buyVersionsArray.join(','),
        bankId: this.bankId
      }
      this.$http.post('/api/createOrder', reqParams)
      .then((res) => {
        this.orderId = res.data.orderId
        this.isShowCheckOrder = true
        this.isShowPayDialog = false
      }, (err) => {
        this.isShowBuyDialog = false
        this.isShowErrDialog = true
      })
    }
  },
  mounted () {
    this.buyNum = 1
    this.buyType = this.buyTypes[0]
    this.versions = [this.versionList[0]]
    this.period = this.periodList[0]
    this.getPrice()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.buy-dialog-title {
  font-size: 16px;
  font-weight: bold;
}
.buy-dialog-btn {
  margin-top: 20px;
}
.buy-dialog-table {
  width: 100%;
  margin-bottom: 20px;
}
.buy-dialog-table td,
.buy-dialog-table th{
  border: 1px solid #e3e3e3;
  text-align: center;
  padding: 5px 0;
}
.buy-dialog-table th {
  background: #4fc08d;
  color: #fff;
  border: 1px solid #4fc08d;
}
</style>
