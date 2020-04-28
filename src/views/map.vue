<template>
  <div class="root" style="background:#ECECEC; padding:10px">
    <a-card class="card" :bordered="false" style="width: 80%">
      <div>
        <div id="chart1"></div>
      </div>
    </a-card>
  </div>
</template>
<script>

import jsonp from 'jsonp';
import echarts from 'echarts';
import 'echarts/map/js/china';

const option = {
  title: {
    text: 'NCP of domestic', // 是否显示标题
    show: true,
    subtext: 'cumulative number of confirmed cases',
    x: 'center',
    
    textStyle: {
      color: '#e74c3c',
      fontStyle: 'normal',
      fontFamily: 'sans-serif'
    }
  },
  tooltip: { //  鼠标移入时的提示信息
    // 类型
    tigger: 'item',
    // b 区域名称 c 合并数值 a 系列名称
    formatter: '地区：{b}<br />感染人口: {c}'
  },

  //  对应的数据
  series: [
    {
      //   地图类型
      type: 'map',
      //  地图内容
      map: 'china',
      // 移动位置
      layoutCenter: ['50%', '50%'],
      layoutSize: 650,
      // 地图显示的数据
      data: [{ name: '', value: '' }],
      // 在地图上添加标签 坐标轴指示器的文本标签。
      label: { // 图形上的标签
        show: true,
        color: '#000000',
        position: 'top'
      },
      
      itemStyle: { // 地图区域的多边形 图形样式。
        borderColor:'#fff' //  '#b1b1b1'
      },
      // 当前视角的缩放比例比例
      zoom: 1.3,
      
      emphasis: { // 高亮状态下的地图颜色
        label: {
          color:'#000000',
          fontSize: '10px'
        },
        itemStyle: {
          areacolor: 'yellow'
        }
      }
    }
  ],
  visualMap: { // 图例
    //   设置类型为分段类型
    type: 'piecewise',
    show: true,
    // 设置段
    pieces: [
      { min: 10001 },
      { min: 1001, max: 10000 },
      { min: 101, max: 1000 },
      { min: 11, max: 100 },
      { min: 1, max: 10 },
      { value: 0 }
    ],
    inRange: {
      // 范围所对应的颜色
      // color:['#fff', 'red']
      color: ['#fff', '#ff7961', '#f05545', '#b71c1c', '#7f0000', '#660208']
    },
    itemWidth: 20,
    itemHeight: 10,
    bottom: 100,
    left: 200
    
  }
};
export default {
  mounted () { // 生命周期
    this.getMsg();
    this.mycharts = echarts.init(document.getElementById('chart1')); // 基于dom，初始化echarts实例
  },
  data () {
    return {
      mycharts: ''
    };
  },
  methods: {
    getMsg () {
      jsonp(
        'http://interface.sina.cn/news/wap/fymap2020_data.d.json?_=1580892522427',
        (err, data) => {
          const lists = data.data.list.map(item => { // map()循环遍历，相当于foreach，但它有返回值。 item是ES6知识
            return {
              name: item.name,
              value: item.value
            };
          });
          // 将数据给到地图
          option.series[0].data = lists;
          
          this.mycharts.setOption(option); // 在mounted加载设置，使用指定的配置项显示图标
        }
      );
    }
  }
};
</script>

<style lang="less" scoped>
.root {
  display: flex;
  justify-content: center;
  align-items: center;
}
#chart1 {
  width: 100%;
  height: 800px;
  text-align: center;
}
</style>
