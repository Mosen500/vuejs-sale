<template>
  <div class="sales-board">
      <div class="sales-board-intro">
        <h2>兴仁盒子粑</h2>
        <p>一是放第一层米浆的时候要将铁盒子放进油锅浸一下，免得粘住；二是当盒子粑炸到要呈金黄色的时候，便要将铁盒子与粑粑脱离，然后用铁盒子的底部挤压一下从铁盒子中脱离的粑粑，让油能把粑粑炸得更彻底，吃的时候口感更好</p>
      </div>
      <div class="sales-board-form">
          <div class="sales-board-line">
              <div class="sales-board-line-left">
                  购买数量：
              </div>
              <div class="sales-board-line-right">
                  <v-counter :max="100" :min="20"></v-counter>
              </div>
          </div>
          <div class="sales-board-line">
              <div class="sales-board-line-left">
                  媒介：
              </div>
              <div class="sales-board-line-right">
                  <v-mul-chooser :selections="versionList"></v-mul-chooser>
              </div>
          </div>
          <div class="sales-board-line">
              <div class="sales-board-line-left">
                  有效时间：
              </div>
              <div class="sales-board-line-right">
                  一个星期
              </div>
          </div>
          <div class="sales-board-line">
              <div class="sales-board-line-left">
                  总价：
              </div>
              <div class="sales-board-line-right">
                  40元
              </div>
          </div>
          <div class="sales-board-line">
              <div class="sales-board-line-left">&nbsp;</div>
              <div class="sales-board-line-right">
                  <div class="button">
                    立即购买
                  </div>
              </div>
          </div>
      </div>
      <div class="sales-board-des">
        <h2>产品说明</h2>
        <p>盒子粑的制作方法，1、将米泡至10小时左右，在用机器磨成浆，2.将一定比例的米浆兑好，将锅里的油烧涨，控制火候，3.把米浆舀在油炸的铁盒子里，这个铁盒子大约深4厘米左右，刚开始舀到铁盒子里的米浆大约要盖过2厘米左右，4.把鲜猪肉丝与葱花、胡椒粉、味精、酱油、盐等佐料拌匀，适量放入铁盒子里，5.再舀米浆铺在上面，放进油锅里炸，直到炸为金黄色，便可以出锅了。子粑的制作很简单，先将一定比例的米浆兑好，将锅里的油烧涨，控制火候，然后把米浆舀在油炸的铁盒子里，这个铁盒子大约深4厘米左右，刚开始舀到铁盒子里的米浆大约要盖过2厘米左右，然后把鲜猪肉丝与葱花、胡椒粉、味精、酱油、盐等佐料拌匀，适量放入铁盒子里，然后再舀米浆铺在上面，放进油锅里炸，直到炸为金黄色，便可以出锅了。炸盒子粑的铁盒子是特制的，长长的手把，盒子呈圆形，所以炸出来的盒子粑也是圆形的。在炸盒子粑的过程中，有两点非常重要，一是放第一层米浆的时候要将铁盒子放进油锅浸一下，免得粘住；二是当盒子粑炸到要呈金黄色的时候，便要将铁盒子与粑粑脱离，然后用铁盒子的底部挤压一下从铁盒子中脱离的粑粑，让油能把粑粑炸得更彻底，吃的时候口感更好。</p>
      </div>
  </div>
</template>

<script>
import VCounter from '../../components/base/counter'
import VMulChooser from '../../components/base/multiplyChooser'
export default {
  components: {
    VCounter,
    VMulChooser
  },
  data () {
    return {
      versionList: [
        {
          label: '淘宝',
          value: 0
        },
        {
          label: '京东',
          value: 1
        },
        {
          label: '天猫',
          value: 2
        },
        {
          label: '聚划算',
          value: 3
        }
      ]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
