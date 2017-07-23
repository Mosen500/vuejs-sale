<template>
  <div class="index-wrap">
    <div class="index-left">
      <div class="index-left-block">
        <h2>特色产品</h2>

        <template v-for="product in productList">
          <h3>{{ product.title}}</h3>
          <ul>
            <li v-for="item in product.list">
              <a :href="item.url">{{ item.name }}</a>
              <span v-if="item.hot" class="hot-tag">HOT</span>
            </li>
          </ul>
          <div v-if="!product.last" class="hr"></div>
        </template>
      </div>
      <div class="index-left-block lastest-news">
        <h2>黔西南动态</h2>
        <ul>
          <li v-for="item in newsList">
            <a :href="item.url" class="new-item">{{ item.title }}</a>
          </li>
        </ul>
      </div>
    </div>
    <div class="index-right">
      <slide-show :slides="slides" :inv="invTime"></slide-show>
      <div class="index-board-list">
        <div
        class="index-board-item"
        v-for="(item, index) in boardList"
        :class="[{'line-last' : index % 2 !== 0}, 'index-board-' + item.id]">
          <div class="index-board-item-inner" >
            <h2>{{ item.title }}</h2>
            <p>{{ item.description }}</p>
            <div class="index-board-button">
              <router-link class="button" :to="{path: 'detail/' + item.toKey}">立即购买</router-link>
              <router-link class="button" :to="{path: 'detail/' + item.toKey}">加入购物车</router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import slideShow from '../components/slideShow'
export default {
  components: {
    slideShow
  },
  created: function () {
    this.$http.get('api/getNewsList')
    .then((res) => {
      this.newsList = res.data
    }, (err) => {
      console.log(err)
    })
  },
  data () {
    return {
      invTime: 2000,
      slides: [
        {
          src: require('../assets/slideShow/pic1.jpg'),
          title: '黔西南景区之万峰林',
          href: 'detail/analysis'
        },
        {
          src: require('../assets/slideShow/pic2.jpg'),
          title: '黔西南景区之马岭河峡谷',
          href: 'detail/count'
        },
        {
          src: require('../assets/slideShow/pic3.jpg'),
          title: '黔西南景区之下午屯',
          href: 'http://www.nipic.com/show/15276944.html'
        },
        {
          src: require('../assets/slideShow/pic4.jpg'),
          title: '黔西南景区之泥凼石林',
          href: 'detail/forecast'
        }
      ],
      boardList: [
        {
          title: '绿色产品',
          description: '绿色产品是纯天然的产品',
          id: 'car',
          toKey: 'analysis',
          saleout: false
        },
        {
          title: '品牌营销',
          description: '品牌营销帮助你的产品更好地找到定位',
          id: 'earth',
          toKey: 'count',
          saleout: false
        },
        {
          title: '下单送达',
          description: '下单送达快速迭代永远保持最前端的速度',
          id: 'loud',
          toKey: 'forecast',
          saleout: true
        },
        {
          title: '服务态度',
          description: '你买的不是产品，而是我们最良心的服务',
          id: 'hill',
          toKey: 'publish',
          saleout: false
        }
      ],
      newsList: [],
      productList: {
        pc: {
          title: '兴义市特产',
          list: [
            {
              name: '兴义耳块粑',
              url: 'http://m.bytravel.cn/produce2/51744E49803357577C91.html'
            },
            {
              name: '兴义羊肉粉',
              url: 'http://m.bytravel.cn/produce/51744E497F8A80897C89/'
            },
            {
              name: '兴义刷把头',
              url: 'http://m.bytravel.cn/produce/51744E495237628A5934/',
              hot: true
            },
            {
              name: '鸡肉汤圆',
              url: 'http://m.bytravel.cn/produce/9E2180896C645706/'
            },
            {
              name: '贵州醇',
              url: 'http://m.bytravel.cn/produce2/8D355DDE9187.html'
            },
            {
              name: '兴义饵馈粑',
              url: 'http://m.bytravel.cn/produce/51744E49997599887C91/',
              hot: true
            }
          ]
        },
        app: {
          title: '兴仁县特产【老家】',
          last: true,
          list: [
            {
              name: '兴仁薏米仁',
              url: 'http://m.bytravel.cn/produce2/51744EC1858F7C734EC1.html'
            },
            {
              name: '一棒雪',
              url: 'http://m.bytravel.cn/produce/4E0068D296EA/',
              hot: true
            },
            {
              name: '兴仁肠旺粉',
              url: 'http://m.bytravel.cn/produce3/xingrenchangwangfen.html'
            },
            {
              name: '兴仁烙锅',
              url: 'http://m.bytravel.cn/produce3/xingrenlaoguo.html'
            },
            {
              name: '兴仁凉水井老腊肉',
              url: 'http://m.bytravel.cn/produce1/6E05954751C96C344E958001814A8089.html'
            }
          ]
        }
      }
    }
  }
}
</script>

<style scoped>
.index-wrap {
  width: 1200px;
  margin: 0 auto;
  overflow: hidden;
}
.index-left {
  float: left;
  width: 300px;
  text-align: left;
}
.index-right {
  float: left;
  width: 900px;
}
.index-left-block {
  margin: 15px;
  background: #fff;
  box-shadow: 0 0 1px #ddd;
}
.index-left-block .hr {
  margin-bottom: 20px;
}
.index-left-block h2 {
  background: #999;
  color: #fff;
  padding: 10px 15px;
  margin-bottom: 20px;
}
.index-left-block h3 {
  padding: 0 15px 5px 15px;
  font-weight: bold;
  color: #222;
}
.index-left-block ul {
  padding: 10px 15px;
}
.index-left-block li {
  padding: 5px;
}
.index-board-list {
  overflow: hidden;
}
.index-board-item {
  float: left;
  width: 400px;
  background: #fff;
  box-shadow: 0 0 1px #ddd;
  padding: 20px;
  margin-right: 20px;
  margin-bottom: 20px;
}
.index-board-item-inner {
  min-height: 125px;
  padding-left: 120px;
}
.index-board-car .index-board-item-inner{
  background: url(../assets/images/1.png) no-repeat;
}
.index-board-loud .index-board-item-inner{
  background: url(../assets/images/2.png) no-repeat;
}
.index-board-earth .index-board-item-inner{
  background: url(../assets/images/3.png) no-repeat;
}
.index-board-hill .index-board-item-inner{
  background: url(../assets/images/4.png) no-repeat;
}
.index-board-item h2 {
  font-size: 18px;
  font-weight: bold;
  color: #000;
  margin-bottom: 15px;
}
.line-last {
  margin-right: 0;
}
.index-board-button {
  margin-top: 20px;
}
.lastest-news {
  min-height: 512px;
}
.hot-tag {
  background: red;
  color: #fff;
}
.new-item {
  display: inline-block;
  width: 230px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
</style>
