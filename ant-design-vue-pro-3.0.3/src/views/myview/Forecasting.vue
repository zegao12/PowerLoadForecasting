<template>
  <div class="app-container">
    <!-- 头部部分 -->
    <div class="head clearfix">
      <h1 class="pulll_left">电力负荷预测系统</h1>
      <div class="menu menu2 pulll_left">
        <ul>
          <li><a href="https://gitee.com/iGaoWei/big-data-view"><a-icon type="sliders" theme="twoTone" style="padding-right: 20px;"/>预测系统</a></li>
          <li><a href="https://gitee.com/iGaoWei/big-data-view"><a-icon type="control" theme="twoTone" style="padding-right: 20px;"/>控制策略</a></li>
          <li><a href="https://gitee.com/iGaoWei/big-data-view"><a-icon type="box-plot" theme="twoTone" style="padding-right: 20px;"/>系统拓扑</a></li>
          <li><a href="https://gitee.com/iGaoWei/big-data-view"><a-icon type="file-pdf" theme="twoTone" style="padding-right: 20px;"/>报表查询</a></li>
          <li><a href="https://gitee.com/iGaoWei/big-data-view"><a-icon type="folder-open" theme="twoTone" style="padding-right: 20px;"/>事件记录</a></li>
          <li><a href="https://gitee.com/iGaoWei/big-data-view"><a-icon type="question-circle" theme="twoTone" style="padding-right: 20px;"/>帮助文档</a></li>
        </ul>
      </div>
      <div class="time" id="showTime">{{ currentTime }}</div>
    </div>
    <!-- 主体部分 -->
    <div class="mainbox">
      <ul class="clearfix nav1">
        <!-- 左侧板块 -->
        <li style="width: 22%">
          <!-- 表格板块 -->
          <div class="box">
            <div class="tit"><span>上月杭州各地电力负荷情况</span><p></p></div>
            <div class="boxnav" style="height: 200px;">
              <table class="table1" width="100%" border="0" cellspacing="0" cellpadding="0">
                <tbody>
                  <tr>
                    <th>市辖区</th>
                    <th>预测负荷</th>
                    <th>实际负荷</th>
                    <th>准确率</th>
                  </tr>
                  <tr>
                    <td>萧山区</td>
                    <td><span class="text-w">1000万</span></td>
                    <td><span class="text-b">900万</span></td>
                    <td><div class="text-d">↑12%</div></td>
                  </tr>
                  <tr>
                    <td>上城区</td>
                    <td><span class="text-w">1000万</span></td>
                    <td><span class="text-b">900万</span></td>
                    <td><div class="text-s">↓12%</div></td>
                  </tr>
                  <tr>
                    <td>拱墅区</td>
                    <td><span class="text-w">1000万</span></td>
                    <td><span class="text-b">900万</span></td>
                    <td><div class="text-d">↑12%</div></td>
                  </tr>
                  <tr>
                    <td>西湖区</td>
                    <td><span class="text-w">1000万</span></td>
                    <td><span class="text-b">900万</span></td>
                    <td><div class="text-s">↓12%</div></td>
                  </tr>
                  <tr>
                    <td>钱塘区</td>
                    <td><span class="text-w">1000万</span></td>
                    <td><span class="text-b">900万</span></td>
                    <td><div class="text-d">↑12%</div></td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
          <div class="box">
            <div class="tit"><span>纬度-月负荷量散点图</span><p></p></div>
            <div class="boxnav" style="height: 250px;">
              <div class="" style="height: 190px" id="echart1">
                <div class="map" id="map">
                  <div ref="aggregateScatterChart" style="height: 100%;width: 100%;"></div>
                </div>
              </div>
              <div class="leidanav">
                <ul class="clearfix">
                  <li><span>文本1</span><p>43</p></li>
                  <li><span>文本2</span><p>100</p></li>
                  <li><span>文本3</span><p>28</p></li>
                  <li><span>文本4</span><p>3</p></li>
                  <li><span>文本5</span><p>150</p></li>
                </ul>
              </div>
            </div>
          </div>
        </li>
        <!-- 中间地图板块 -->
        <li style="width: 56%">
          <div class="box">
            <div class="boxnav mapc" style="height: 550px; position: relative">
              <div class="mapnav">
                <ul>
                  <li><div><span>数据1</span><p>40%</p></div></li>
                  <li><div><span>数据2</span><p>12%</p></div></li>
                  <li><div><span>数据3</span><p>80</p></div></li>
                  <li><div><span>数据4</span><p>124</p></div></li>
                  <li><div><span>数据5</span><p>10%</p></div></li>
                </ul>
              </div>
              <div class="mapnav2">
                <div class="box">
                  <div class="tit"><span>杭州月负荷量预测</span><p></p></div>
                  <div class="boxnav" style="height: 230px;" id="sysx">
                    <!-- <div class="map"></div> -->
                    <div ref="hzLineChart" style="height: 250px;width: 100%;"></div>
                  </div>
                  <!-- <div class="leidanav leidanav3" style="margin-bottom: 15px;">
                    <ul class="clearfix">
                      <li><span>业务笔数</span><p>128</p></li>
                      <li><span>业务收益</span><p>100</p></li>
                      <li><span>业务笔数</span><p>28</p></li>
                      <li><span>业务收益</span><p>28</p></li>
                    </ul>
                  </div> -->
                </div>
              </div>
              <div class="map" id="map">
                <!-- width: 868px; -->
                <div ref="mapChart" style="height: 100%;width: 100%;"></div>
              </div>
            </div>
          </div>
        </li>
        <!-- 右侧板块 -->
        <li style="width: 22%">
          <div class="box" style="text-align: center;">
            <div class="tit"><span>当月负荷异常次数/<br>负荷异常最多区域</span><p></p></div>
    <div style="height: 180px; display: flex; justify-content: space-around;">
        <div style="text-align: left;">
            <div style="display: inline-flex; align-items: baseline;">
                <div class="num" style="font-size: 60px; font-weight: bold; margin-right: 4px;">17</div>
                <div style="font-size: 36px;color: white;font-weight: 500;">次</div>
            </div>
            <div style="margin-top: 20px; font-size: 14px; color: #ccc;">
                <p>同比:0</p>
                <p>环比:0</p>
            </div>
        </div>
        <div style="text-align: left;">
            <div style="display: inline-flex; align-items: baseline;">
                <div class="num" style="font-size: 60px; font-weight: bold; margin-right: 4px;">5</div>
                <div style="font-size: 36px;color: white;font-weight: 500;">次/月</div>
            </div>
            <div style="margin-top: 20px; font-size: 14px; color: #ccc;">
                <p>区域: GENESE</p>
            </div>
        </div>
    </div>
</div>
          <div class="box">
            <div class="tit"><span>负荷特征相关性矩阵</span><p></p></div>
            <div class="map" id="map">
              <div ref="correlationChart" style="height: 245px;width: 100%;"></div>
            </div>
            <!-- <div class="boxnav" style="height: 250px;">
              <div style="height: 200px; float: left; width: 40%; padding: 0 5px;">
                <div class="tit02 text-b">热门话题榜</div>

                <div class="huati">
                  <ul>
                    <li>1.数据分析  <span class="text-s">↑2167</span></li>
                    <li>2.云存储     <span class="text-s">↑2167</span></li>
                    <li>3.视觉分析   <span class="text-d">↓2167</span></li>
                    <li>4.海量词库   <span class="text-d">↓2167</span></li>
                    <li>5.云词典      <span class="text-d">↓2167</span></li>
                  </ul>
                </div>
              </div>
              <div style="height: 200px; float: left; width: 60%">
                <div class="text-b tit02" style="text-align: center;">关键词 — 云</div>
                <div class="tagcloud">
                  <a class="b01 co01" href="https://gitee.com/iGaoWei/big-data-view">大数据</a>
                  <a class="b02 co02" href="https://gitee.com/iGaoWei/big-data-view">大数据</a>
                  <a class="b03 co05" href="https://gitee.com/iGaoWei/big-data-view">大数据</a>
                  <a class="b04 co02" href="https://gitee.com/iGaoWei/big-data-view">大数据</a>
                  <a class="b03 co05" href="https://gitee.com/iGaoWei/big-data-view">大数据</a>
                </div>
              </div>
            </div> -->
          </div>
        </li>
      </ul>
      <div class="box" style="padding: 20px 0;">
        <ul class="clearfix nav2 ">
          <li style="width: 25%;height: 400px;">
            <div class="tit"><span>杭州各区过去24小时负荷分布</span><p></p></div>
            <!-- <div class="">
              <div style="float: left; width: 50%; height: 170px" id="fb01"></div>
              <div style="float: left; width: 50%; height: 170px" id="fb02"></div>
            </div> -->
            <div class="ftechart" style="height: 300px;">
              <div ref="hzPieChart" style="height: 100%;width: 100%;"></div>
            </div>
            <!-- <div class="leidanav leidanav2">
              <ul class="clearfix">
                <li><span>总人数</span><p>128</p></li>
                <li><span>男职员</span><p>100</p></li>
                <li><span>女职员</span><p>28</p></li>
              </ul>
            </div> -->
          </li>
          <li style="width:25%;height: 400px;" >
            <div class="tit"><span>负荷预测准确率</span><p></p></div>
            <div class="ftechart" id="echart4" style="height: 300px;">
              <div ref="hzAccuracyChart" style="height: 100%;width: 100%;"></div>
            </div>
          </li>
          <li style="width:50%">
            <div class="tit"><span>用能趋势</span><p></p></div>
            <div class="ftechart" style="height: 300px;">
              <div ref="ultraShortTermChart" style="height: 100%;width: 100%;"></div>
            </div>
            <!-- <div style="height:100%;display: flex; align-items: center;">
              <div style="float: left; width: 50%; height: 100%" class="wancheng">
                <div><span>已完成人数</span>
                  <h3>1835<i>人</i></h3></div>
                <div class="yuan">
                  <span>19%</span>
                </div>
              </div>
              <div style="float: left; width: 50%; height: 50%" id="myd1"></div>
            </div> -->
          </li>
          <!-- <li style="width:25%">
            <div class="tit"><span>板块标题</span><p></p></div>

            <div class="">
              <div style="float: left; width: 50%; height: 200px" id="fb03"></div>
              <div style="float: left; width: 50%; height: 200px" id="fb04"></div>
            </div>
          </li> -->
        </ul>
      </div>
    </div>
  </div>
</template>

  <script>
  import * as echarts from 'echarts'
  import chinaJson from '@/assets/geo/china.json'
  export default {
    data () {
      return {
        currentTime: ''
      }
    },
    mounted () {
      this.updateTime()
      this.initChart()
      this.initGeoLoadScatterCharts()
      this.initHangzhouLoadLineChart()
      this.initHzDistrictPieChart()
      this.initHzAccuracyRingChart()
      this.initUltraShortTermChart()
      this.initLoadCorrelationChart()
      setInterval(this.updateTime, 1000)
    },
    methods: {
      updateTime () {
        const dt = new Date()
        const y = dt.getFullYear()
        const mt = dt.getMonth() + 1
        const day = dt.getDate()
        const h = dt.getHours()
        const m = dt.getMinutes()
        const s = dt.getSeconds()
        this.currentTime = `${y}/${mt}/${day} ${h}:${m}:${s}`
      },
      initChart () {
  const chart = echarts.init(this.$refs.mapChart)

  // 注册中国地图
  echarts.registerMap('china', chinaJson)

  const option = {
    tooltip: {
      trigger: 'item',
      formatter: '{b}<br/>负荷值: {c}'
    },
    visualMap: {
      min: 0,
      max: 500,
      right: 20,
      top: 'bottom',
      text: ['高', '低'],
      inRange: {
        color: ['#00CED1', '#FFD700', '#FF4500']
      },
      textStyle: {
        color: '#fff'
      }
    },
    series: [
      {
        name: '负荷预测',
        type: 'map',
        map: 'china',
        roam: true,
        label: {
          show: true,
          color: '#fff'
        },
        emphasis: {
          label: {
            color: '#fff'
          },
          itemStyle: {
            areaColor: '#1E90FF'
          }
        },
        data: [
        { name: '北京市', value: 420 },
{ name: '天津市', value: 280 },
{ name: '河北省', value: 380 },
{ name: '山西省', value: 240 },
{ name: '内蒙古自治区', value: 260 },
{ name: '辽宁省', value: 220 },
{ name: '吉林省', value: 180 },
{ name: '黑龙江省', value: 190 },
{ name: '上海市', value: 450 },
{ name: '江苏省', value: 480 },
{ name: '浙江省', value: 460 },
{ name: '安徽省', value: 270 },
{ name: '福建省', value: 300 },
{ name: '江西省', value: 210 },
{ name: '山东省', value: 400 },
{ name: '河南省', value: 350 },
{ name: '湖北省', value: 290 },
{ name: '湖南省', value: 260 },
{ name: '广东省', value: 500 },
{ name: '广西壮族自治区', value: 170 },
{ name: '海南省', value: 120 },
{ name: '重庆市', value: 230 },
{ name: '四川省', value: 320 },
{ name: '贵州省', value: 140 },
{ name: '云南省', value: 160 },
{ name: '西藏自治区', value: 50 },
{ name: '陕西省', value: 190 },
{ name: '甘肃省', value: 110 },
{ name: '青海省', value: 80 },
{ name: '宁夏回族自治区', value: 100 },
{ name: '新疆维吾尔自治区', value: 130 },
{ name: '香港特别行政区', value: 180 },
{ name: '澳门特别行政区', value: 100 }
        ]
      }
    ]
  }

  chart.setOption(option)
  window.addEventListener('resize', () => chart.resize())
      },
      initGeoLoadScatterCharts () {
  const chartDom = this.$refs.aggregateScatterChart
  const myChart = echarts.init(chartDom)

  // 模拟城市及其纬度和月负荷值
  const cities = [
    { name: '哈尔滨', lat: 45.75, load: 1200 },
    { name: '北京', lat: 39.9, load: 1800 },
    { name: '上海', lat: 31.2, load: 2400 },
    { name: '广州', lat: 23.1, load: 2700 },
    { name: '成都', lat: 30.6, load: 2100 },
    { name: '武汉', lat: 30.5, load: 2300 },
    { name: '深圳', lat: 22.5, load: 2600 },
    { name: '西安', lat: 34.3, load: 2000 },
    { name: '昆明', lat: 25.0, load: 1700 },
    { name: '乌鲁木齐', lat: 43.8, load: 1300 },
    { name: ' 天津 ', lat: 39.1, load: 1700 },
{ name: ' 重庆 ', lat: 29.5, load: 2000 },
{ name: ' 沈阳 ', lat: 41.8, load: 1500 },
{ name: ' 南京 ', lat: 32.0, load: 2200 },
{ name: ' 杭州 ', lat: 30.2, load: 2200 },
{ name: ' 济南 ', lat: 36.6, load: 1900 },
{ name: ' 郑州 ', lat: 34.7, load: 1900 },
{ name: ' 合肥 ', lat: 31.8, load: 1800 },
{ name: ' 福州 ', lat: 26.0, load: 1800 },
{ name: ' 南昌 ', lat: 28.6, load: 1700 },
{ name: ' 长沙 ', lat: 28.2, load: 1900 },
{ name: ' 南宁 ', lat: 22.8, load: 1600 },
{ name: ' 海口 ', lat: 20.0, load: 1400 },
{ name: ' 贵阳 ', lat: 26.5, load: 1500 },
{ name: ' 兰州 ', lat: 36.0, load: 1400 },
{ name: ' 西宁 ', lat: 36.6, load: 1200 },
{ name: ' 银川 ', lat: 38.4, load: 1300 },
{ name: ' 石家庄 ', lat: 38.0, load: 1700 },
{ name: ' 太原 ', lat: 37.8, load: 1500 },
{ name: ' 呼和浩特 ', lat: 40.8, load: 1400 },
{ name: ' 长春 ', lat: 43.8, load: 1300 },
{ name: ' 大连 ', lat: 38.9, load: 1600 },
{ name: ' 青岛 ', lat: 36.0, load: 1800 },
{ name: ' 苏州 ', lat: 31.3, load: 2000 },
{ name: ' 宁波 ', lat: 29.8, load: 1900 },
{ name: ' 厦门 ', lat: 24.4, load: 1600 },
{ name: ' 佛山 ', lat: 23.0, load: 2000 },
{ name: ' 东莞 ', lat: 23.0, load: 1900 }
  ]

  const data = cities.map(city => ({
    name: city.name,
    value: [city.lat, city.load]
  }))

  const option = {
    backgroundColor: 'transparent',
    tooltip: {
      trigger: 'item',
      formatter: p => `城市: ${p.name}<br/>纬度: ${p.value[0]}°<br/>负荷: ${p.value[1]} MW`
    },
    grid: {
      left: '10%',
      right: '10%',
      bottom: '10%',
      top: '20%'
    },
    xAxis: {
      name: '纬度 (°)',
      nameTextStyle: { color: '#ccc' },
      axisLine: { lineStyle: { color: '#aaa' } },
      axisLabel: { color: '#ccc' },
      splitLine: { lineStyle: { color: '#444', type: 'dashed' } }
    },
    yAxis: {
      name: '月负荷量 (MW)',
      nameTextStyle: { color: '#ccc' },
      axisLine: { lineStyle: { color: '#aaa' } },
      axisLabel: { color: '#ccc' },
      splitLine: { lineStyle: { color: '#444', type: 'dashed' } }
    },
    series: [
      {
        name: '城市负荷',
        type: 'scatter',
        symbolSize: 12,
        itemStyle: {
          color: '#1de9b6'
        },
        label: {
          show: true,
          position: 'top',
          formatter: p => p.name,
          color: '#fff',
          fontSize: 12
        },
        data: data
      }
    ]
  }

  myChart.setOption(option)
      },
      initHangzhouLoadLineChart () {
  const chartDom = this.$refs.hzLineChart
  const myChart = echarts.init(chartDom)

  const months = ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月']
  const loadData = [1200, 1350, 1600, 1750, 1900, 2100, 2500, 2700, 2400, 2200, 1800, 1500]

  const option = {
    backgroundColor: 'transparent',
    tooltip: {
      trigger: 'axis',
      formatter: params => {
        const item = params[0]
        return `${item.axisValue}<br/>负荷量: ${item.data} MW`
      }
    },
    xAxis: {
      type: 'category',
      data: months,
      axisLine: { lineStyle: { color: '#aaa' } },
      axisLabel: { color: '#ccc' }
    },
    yAxis: {
      type: 'value',
      name: '负荷量 (MW)',
      nameTextStyle: { color: '#ccc' },
      axisLine: { lineStyle: { color: '#aaa' } },
      axisLabel: { color: '#ccc' },
      splitLine: { lineStyle: { color: '#444', type: 'dashed' } }
    },
    series: [
      {
        name: '负荷量',
        type: 'line',
        smooth: true,
        symbol: 'circle',
        symbolSize: 8,
        lineStyle: {
          color: '#00c0ff',
          width: 3
        },
        itemStyle: {
          color: '#00e3ff'
        },
        areaStyle: {
          color: 'rgba(0, 192, 255, 0.2)'
        },
        data: loadData
      }
    ]
  }

  myChart.setOption(option)
      },
      initHzDistrictPieChart () {
  const chartDom = this.$refs.hzPieChart
  const myChart = echarts.init(chartDom)

  // 模拟杭州各区24小时累计负荷（单位 MW）
  const data = [
    { name: '上城区', value: 350 },
    { name: '拱墅区', value: 420 },
    { name: '西湖区', value: 390 },
    { name: '滨江区', value: 310 },
    { name: '萧山区', value: 480 },
    { name: '余杭区', value: 460 },
    { name: '临平区', value: 330 },
    { name: '钱塘区', value: 300 }
  ]

  const option = {
    backgroundColor: 'transparent',
    tooltip: {
      trigger: 'item',
      formatter: '{b}<br/>负荷: {c} MW ({d}%)'
    },
    legend: {
      orient: 'vertical',
      right: '5%',
      top: 'middle',
      textStyle: { color: '#ccc' }
    },
    series: [
      {
        name: '负荷分布',
        type: 'pie',
        radius: ['35%', '60%'],
        center: ['45%', '55%'],
        avoidLabelOverlap: false,
        itemStyle: {
          borderColor: '#111',
          borderWidth: 2
        },
        label: {
          show: true,
          color: '#fff',
          formatter: '{b}\n{d}%'
        },
        labelLine: {
          length: 20,
          length2: 10,
          lineStyle: {
            color: '#888'
          }
        },
        data: data
      }
    ]
  }

  myChart.setOption(option)
  window.addEventListener('resize', () => myChart.resize())
      },
      initHzAccuracyRingChart () {
  const chartDom = this.$refs.hzAccuracyChart
  const myChart = echarts.init(chartDom)

  const districtAccuracy = [
    { name: '上城区', value: 96.5, color: '#4FC3F7' },
    { name: '西湖区', value: 97.8, color: '#81C784' },
    { name: '拱墅区', value: 96.9, color: '#FFD54F' },
    { name: '滨江区', value: 98.1, color: '#BA68C8' },
    { name: '萧山区', value: 97.3, color: '#E57373' },
    { name: '余杭区', value: 96.7, color: '#4DD0E1' },
    { name: '临平区', value: 97.0, color: '#F06292' },
    { name: '钱塘区', value: 96.4, color: '#A1887F' }
  ]

  const totalAccuracy = 97.2

  const baseRadius = 40 // 最内圈起始半径
  const gap = 7 // 环与环之间的间距
  const barWidth = 4 // 环本身的厚度（细）

  const series = districtAccuracy.map((d, i) => ({
    type: 'pie',
    name: d.name,
    radius: [`${baseRadius + i * gap}%`, `${baseRadius + i * gap + barWidth}%`],
    center: ['50%', '50%'],
    data: [
      {
        value: d.value,
        name: d.name,
        itemStyle: { color: d.color }
      },
      {
        value: 100 - d.value,
        name: '',
        tooltip: { show: false },
        itemStyle: {
          color: 'transparent'
        },
        label: { show: false }
      }
    ],
    label: { show: false },
    hoverAnimation: false
  }))

  const option = {
    backgroundColor: 'transparent',
    title: [
      {
        text: '过去24H',
        left: 'center',
        top: '43%',
        textStyle: {
          color: '#ccc',
          fontSize: 14,
          align: 'center'
        }
      },
      {
        text: `${totalAccuracy}%`,
        left: 'center',
        top: '50%',
        textStyle: {
          color: '#1de9b6',
          fontSize: 28,
          fontWeight: 'bold',
          align: 'center'
        }
      }
    ],
    tooltip: {
      trigger: 'item',
      formatter: '{b}<br/>预测准确率: {c}%'
    },
    series
  }

  myChart.setOption(option)
  window.addEventListener('resize', () => myChart.resize())
      },
      initUltraShortTermChart () {
      const chartDom = this.$refs.ultraShortTermChart
      const myChart = echarts.init(chartDom)
      const option = {
  tooltip: {
    trigger: 'axis'
  },
  legend: {
    data: ['当月', '上月'],
    textStyle: {
      color: 'white'
    }
  },
  toolbox: {
    show: true,
    feature: {
      dataView: { show: true, readOnly: false },
      magicType: { show: true, type: ['line', 'bar'] },
      restore: { show: true },
      saveAsImage: { show: true }
    }
  },
  calculable: true,
  xAxis: [
    {
      type: 'category',
      data: ['1日', '3日', '5日', '7日', '9日', '11日', '13日', '15日', '17日', '19日', '21日', '23日', '25日', '27日', '29日', '31日'],
      axisLabel: {
        color: 'white'
    }
  }
  ],
  yAxis: [
    {
      type: 'value',
      name: '萧山区(kw·h)',
      nameLocation: 'end',
      nameGap: 30,
      nameTextStyle: {
        color: 'white',
        fontSize: 14
      },
      splitLine: {
                show: true, // 是否显示分隔线，默认为 true
                lineStyle: {
                    color: 'rgba(128,128,128,0.5)',
                    width: 1, // 分隔线宽度
                    type: 'solid' // 分隔线样式，'solid' 为实线，'dashed' 为虚线
                }
            }
    }
  ],
  series: [
    {
      name: '当月',
      type: 'bar',
      data: [
5200, 12800, 3400, 16500, 4100, 14300, 7800, 17900, 3200, 15600, 6700, 13200, 9100, 17100, 4500, 16200,
8300, 11800, 12400, 17600, 3900, 13700, 7400, 15900, 5800, 18100, 4900, 14700, 8600, 16300, 6100
],
      lineStyle: {
        color: 'rgb(46,200,206)'
      },
      itemStyle: {
        color: 'rgb(46,200,206)'
      }
    },
    {
      name: '上月',
      type: 'bar',
      data: [
3600, 14900, 5300, 16800, 3900, 12100, 8700, 17300, 4400, 15200, 7200, 13900, 10200, 16600, 4700, 15800,
9500, 11400, 13100, 17800, 3700, 14200, 7900, 16400, 6300, 18300, 5100, 15100, 9300, 16700, 6600
],

      lineStyle: {
        color: 'rgba(174,164,231) '
      },
      itemStyle: {
        color: 'rgba(174,164,231) '
      }
    }
  ]
}
      myChart.setOption(option)
      this.ultraShortTermChart = myChart
      },
      initLoadCorrelationChart () {
  const chartDom = this.$refs.correlationChart
  const myChart = echarts.init(chartDom)

  // 模拟特征名称和相关性数据
  const features = ['负荷', '温度', '湿度', '风速', '光照', '节假日', '时间段']
  const data = []

  // 随机生成对称的相关性矩阵
  for (let i = 0; i < features.length; i++) {
    for (let j = 0; j < features.length; j++) {
      const value = i === j ? 1 : parseFloat((Math.random() * 2 - 1).toFixed(2))
      data.push([i, j, value])
    }
  }

  const option = {
    backgroundColor: 'transparent',
    tooltip: {
      position: 'top',
      formatter: ({ value }) =>
        `特征1: ${features[value[0]]}<br/>特征2: ${features[value[1]]}<br/>相关性: ${value[2]}`
    },
    xAxis: {
      type: 'category',
      data: features,
      splitArea: { show: true },
      axisLine: { lineStyle: { color: '#aaa' } },
      axisLabel: { color: '#ccc' }
    },
    yAxis: {
      type: 'category',
      data: features,
      splitArea: { show: true },
      axisLine: { lineStyle: { color: '#aaa' } },
      axisLabel: { color: '#ccc' }
    },
    visualMap: {
      min: -1,
      max: 1,
      calculable: true,
      orient: 'horizontal',
      left: 'center',
      bottom: '10%',
      inRange: {
        color: ['#313695', '#4575b4', '#74add1', '#e0f3f8', '#fee090', '#f46d43', '#d73027']
      },
      textStyle: { color: '#ccc' }
    },
    series: [{
      name: '相关性',
      type: 'heatmap',
      data: data,
      label: {
        show: true,
        color: '#fff',
        formatter: ({ value }) => value[2].toFixed(2)
      },
      emphasis: {
        itemStyle: {
          shadowBlur: 10,
          shadowColor: 'rgba(0, 0, 0, 0.5)'
        }
      }
    }]
  }

  myChart.setOption(option)
}

    }
  }
  </script>

  <style scoped>
  /* 以下是从 style.css 复制过来的样式 */
  * {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  *,
  body {
    padding: 0px;
    margin: 0px;
    font-family: "微软雅黑";
  }
  body {
    color: #fff;
    font-size: 16px;
    background: #033c76;
    background: -webkit-radial-gradient(50% 35%, farthest-corner, #034f8e, #034987, #02366d, #002353);
    background: radial-gradient(50% 35%, farthest-corner, #034f8e, #034987, #02366d, #002353);
  }
  html,
  body {
    height: 100%;
  }
  li {
    list-style-type: none;
  }
  table {}
  i {
    margin: 0px;
    padding: 0px;
    text-indent: 0px;
  }
  img {
    border: none;
    max-width: 100%;
  }
  a {
    text-decoration: none;
    color: #fff;
  }
  a.active,
  a:focus {
    outline: none !important;
    text-decoration: none;
  }
  ol,
  ul,
  p,
  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    padding: 0;
    margin: 0;
  }
  a:hover {
    color: #06c;
    text-decoration: none !important;
  }
  .clearfix:after,
  .clearfix:before {
    display: table;
    content: " ";
  }
  .clearfix:after {
    clear: both;
  }
  .pulll_left {
    float: left;
  }
  .pulll_right {
    float: right;
  }
  i {
    font-style: normal;
  }
  .text-w {
    color: #ffe400;
  }
  .text-d {
    color: #ff6316;
  }
  .text-s {
    color: #14e144;
  }
  .text-b {
    color: #07e5ff;
  }

  .head {
    position: relative;
    height: 90px;
    margin: 0 15px;
    padding-right: 60px;
  }
  .head h1 {
    font-size: 30px;
    letter-spacing: -2px;
    text-align: center;
    line-height: 90px;
    padding-right: 55px;
    color: #daf9ff;
  }
  .head .menu {}
  .head .menu ul {
    font-size: 0;
  }

  .head .menu li {
    display: inline-block;
    position: relative;
    margin: 25px 15px;
  }
  .head .menu li a {
    display: block;
    font-size: 18px;
    color: #fff;
    line-height: 40px;
    padding: 0 15px;
  }
  .head .time {
    position: absolute;
    right: 0;
    line-height: 90px;
  }

  .menu li:before,
  .menu li:after {
    position: absolute;
    width: 10px;
    height: 5px;
    opacity: 0.4;
    content: "";
    border-top: 2px solid #02a6b5;
    top: -1px;
    border-radius: 2px;
  }
  .menu li:before,
  .menu li a:before {
    border-left: 2px solid #02a6b5;
    left: -1px;
  }
  .menu li:after,
  .menu li a:after {
    border-right: 2px solid #02a6b5;
    right: -1px;
  }
  .menu li a {
    position: relative;
  }
  .menu li a:before,
  .menu li a:after {
    position: absolute;
    width: 10px;
    height: 5px;
    opacity: 0.4;
    content: "";
    border-bottom: 2px solid #02a6b5;
    bottom: -1px;
    border-radius: 2px;
  }

  .head .menu li a:hover {
    color: #f4e925;
  }
  .menu li a:hover:before,
  .menu li a:hover:after,
  .menu li:hover:before,
  .menu li:hover:after {
    border-color: #f4e925;
    opacity: 1;
  }

  .mainbox {
    padding: 0px 10px;
  }
  .nav1 {
    margin-left: -6px;
    margin-right: -6px;
  }
  .nav1>li {
    padding: 0 6px;
    float: left;
  }

  .box {
    border: 1px solid rgba(7, 118, 181, 0.5);
    box-shadow: inset 0 0 10px rgba(7, 118, 181, 0.4);
    margin-bottom: 12px;
    position: relative;
  }
  .tit{ display: flex; align-items: flex-end;color: white;}
.tit span{ background: url(../../assets/images/line1.png) no-repeat bottom right; font-size: 20px; white-space: nowrap; padding-bottom: 10px; padding-right: 20px;}
.tit p{ background: url(../../assets/images/line2.png) no-repeat bottom right; width: 100%; height: 13px; margin-bottom: 5px; opacity: .5}
  .box:before {
    width: 100%;
    height: 1px;
    content: "";
    position: absolute;
    left: 0;
    bottom: -1px;
    background: linear-gradient(to right, #076ead, #4ba6e0, #076ead);
    box-shadow: 0 0 5px rgba(131, 189, 227, 1);
    opacity: 0.6;
  }
  .box:before {
    top: -1px;
  }

  .boxnav {
    padding: 0px;
  }
  .nav2 {}
  .nav2>li:first-child {
    border: none;
  }
  .nav2>li {
    float: left;
    border-left: 1px solid rgba(7, 118, 181, 0.2);
    height: 240px;
    padding: 0 10px 10px 10px;
  }
  .tit {
    font-size: 16px;
    font-weight: 500;
    position: relative;
    padding-left: 15px;
  }
  .tit:before {
    left: 3px;
    top: 8px;
  }
  ._icon
  {
    margin: 2px;
  }
  .ftechart {
    height: 200px;
  }

  .table1 th {
    border-bottom: 1px solid #407abd;
    font-size: 14px;
    text-align: center;
    padding: 6px 0;
    color: rgba(255, 255, 255, 0.8);
  }
  .table1 td {
    border-bottom: 1px dotted #407abd;
    font-size: 12px;
    padding: 6px 0;
    text-align: center;
    color: rgba(255, 255, 255, 0.6);
  }
  .table1 tr:last-child td {
    border: none;
  }
  .mapc {
    background: url(../../assets/images/bg3.png) no-repeat center center;
    background-size: 100% 100%;
  }
  .map {
    position: relative;
  height: 100%;
  padding-left: 0; /* 避免偏移 */
  }
  .map img {}
  .mapnav {
    position: absolute;
    z-index: 10;
  }
  .mapnav div {
    background: url(../../assets/images/bg4.png) no-repeat;
    background-size: 100% auto;
    width: 110px;
    text-align: center;
    padding: 20px 0;
    line-height: 120%;
  }
  .mapnav div span {
    font-size: 14px;
    opacity: 0.6;
  }
  .mapnav div p {
    font-size: 20px;
    font-weight: bold;
    padding-top: 5px;
  }
  .mapnav li {
    float: left;
    margin-right: 6px;
  }

  .leidanav {
    margin-top: -5px;
  }
  .leidanav li {
    float: left;
    width: 20%;
    text-align: center;
    border-left: 1px solid rgba(255, 255, 255, 0.1);
  }
  .leidanav2 li {
    width: 33.3333%;
  }
  .leidanav3 li {
    width: 25%;
  }
  .leidanav li:first-child {
    border-left: none;
  }
  .leidanav span {
    font-size: 12px;
    opacity: 0.6;
  }

  .leidanav p {
    font-size: 18px;
    color: #26a6ff;
  }
  .mapnav2 {
    position: absolute;
    left: 10px;
    bottom: 0px;
    width: 40%;
    z-index: 10;
  }
  .echarts-map-container {
  width: 100%;
  height: 100%;
}
  .mapnav2 .box {}
  .ybp {
    width: 100%;
  }
  .ybp li {
    float: left;
    width: 50%;
    height: 120px;
  }
  .duibi li {
    float: left;
    width: 25%;
    height: 200px;
    padding: 0;
    border: none;
  }

  .btn {
    position: absolute;
    border-radius: 2px;
    padding: 4px 20px;
    opacity: 0.8;
  }
  .btn1 {
    border: 1px solid rgba(255, 255, 255, 0.5);
    background: #388665;
    left: 35%;
    top: 30%;
  }
  .btn2 {
    border: 1px solid rgba(255, 255, 255, 0.5);
    background: #297cc7;
    right: 32%;
    top: 60%;
  }
  .btn:hover {
    color: #fff;
    opacity: 1;
  }
  .btn1:before,
  .btn2:before {
    position: absolute;
    content: '';
    width: 50px;
    height: 1px;
    background: #fff;
  }
  .btn1:before {
    transform: rotate(30deg);
    right: -65%;
    top: 100%;
  }
  .btn2:before {
    transform: rotate(30deg);
    left: -65%;
    top: -10%;
  }
  .tit02 {
    font-size: 14px;
    padding: 10px 0;
  }

  .tagcloud {
    width: 100%;
    height: 90% !important;
    overflow: hidden;
    position: relative;
  }
  .tagcloud a {
    display: block;
    border-radius: 50%;
    color: #fff;
    font-weight: bold;
    font-size: 14px;
    text-decoration: none;
    text-align: center;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .b01 {
    width: 50px;
    height: 50px;
  }
  .b02 {
    width: 80px;
    height: 80px;
  }
  .b03 {
    width: 60px;
    height: 60px;
  }
  .b04 {
    width: 70px;
    height: 70px;
  }
  .co01 {
    border: 2px solid rgba(5, 118, 254, 1);
    box-shadow: inset 0 0 20px rgba(5, 118, 254, 1);
  }
  .co02 {
    border: 2px solid rgba(238, 255, 65, 1);
    box-shadow: inset 0 0 20px rgba(238, 255, 65, 1);
  }
  .co03 {
    border: 2px solid rgba(26, 121, 181, 1);
    box-shadow: inset 0 0 20px rgba(26, 121, 181, 1);
  }
  .co04 {
    border: 2px solid rgba(1, 187, 181, 1);
    box-shadow: inset 0 0 20px rgba(1, 187, 181, 1);
  }
  .co05 {
    border: 2px solid rgba(255, 138, 0, 1);
    box-shadow: inset 0 0 20px rgba(255, 138, 0, 1);
  }

  .huati {
    padding-top: 20px;
  }
  .huati li {
    font-size: 12px;
    line-height: 230%;
  }

  .wancheng {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .wancheng span {
    font-size: 14px;
    color: #fff;
  }
  .wancheng h3 {
    font-size: 20px;
    color: #00b4ff;
  }
  .wancheng h3 i {
    font-size: 12px;
    color: #fff;
  }
  .yuan {
    padding: 5px;
    border-radius: 100%;
    margin-left: 10px;
    border: 2px solid rgba(0, 99, 169, 0.8);
  }
  .yuan span {
    width: 60px;
    height: 60px;
    border-radius: 100%;
    background: rgba(0, 99, 169, 0.8);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 20px;
  }
  .app-container {
    background-image: url('D:/code_2025/1/PowerLoadForecasting/ant-design-vue-pro-3.0.3/src/assets/images/back.png');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    color: #1890ff;
    font-family: Arial, sans-serif;
    min-height: 100vh;
    overflow-y: auto;
  }
  .pngmap
  {
    background-image: url(../../assets/images/R.png);
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
  }
  @font-face {
  font-family: "myfont";
  src: url(../../assets/font/DS-DIGIT.TTF);
}
.num {
    font-family: "ElectronicFont", sans-serif; /* 使用字体 */
    font-size: 50px;        /* 字体大小 */
    color: #00deff;         /* 字体颜色 */
    text-shadow: 0 0 5px #00deff; /* 发光效果 */
}
.ylfwbox ol span {
  font-size: 24px;
  color: #00deff;
  text-shadow: 0 0 5px #00deff;
  font-family: electronicFont;
}

  </style>
