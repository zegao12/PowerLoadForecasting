<template>
  <div class="app-container">

    <div class="head clearfix">
      <h1 class="" style="font-size: 30px;">基于大语言模型的电力负荷预测</h1>
    </div>
    <ul class="clearfix nav1" style="width: 1625px;">
      <li style="width: 26%;">
        <div class="box">
          <div class="tit"><span>日负荷热力图</span><p></p></div>
          <div class="chart" ref="dailyLoadHeatmap"></div>
        </div>
        <div class="box">
          <div class="tit"><span>超短时功率预测曲线(4h)</span><p></p></div>
          <div class="chart" ref="ultraShortTermChart"></div>
        </div>
        <div class="box">
          <div class="tit" style="color: white;"><span>模型性能对比</span><p></p></div>
          <div class="chart" ref="modelRadarChart"></div>
        </div>
      </li>
      <li style="width: 48%;">
        <div class="box">
          <div class="box" style="position: relative">
            <div class="map">
              <div class="map1"><img src="../../assets/images/lbx.png"></div>
              <div class="map2"><img src="../../assets/images/jt.png"></div>
              <div class="map3"><img src="../../assets/images/map.png"></div>
            </div>
            <div class="" id="map" style="height: 720px; position: relative; z-index: 100"></div>
          </div>
        </div>
        <div class="box">
          <div class="tit" style="color: white;"><span>超短时功率预测曲线(4h)</span><p></p></div>
          <div class="chart" ref="shortTermChart"></div>
        </div>
      </li>
      <li style="width: 26%;">
        <div class="box">
          <div class="tit" style="color: white;"><span>多站点负荷预测</span><p></p></div>
          <div class="chart" ref="multiStationLoadChart"></div>
        </div>
        <div class="box">
          <div class="tit" style="color: white;"><span>预测进度</span><p></p></div>
          <div class="chart" ref="gaugeChart"></div>
        </div>
        <div class="box">
          <div class="tit"><span>预测误差(4h)</span><p></p></div>
          <table class="stats-table" >
            <tr><td>均方根</td><td style="color: rgb(27,243,248);">0.12</td></tr>
            <tr><td>平均绝对误差</td><td style="color: rgb(27,243,248);">0.09</td></tr>
            <tr><td>相关性系数</td><td style="color: rgb(27,243,248);">0.01</td></tr>
            <tr><td>最大预测误差</td><td style="color: rgb(27,243,248);">49.1</td></tr>
            <tr><td>合格率</td><td style="color: rgb(27,243,248);">90.15%</td></tr>
          </table>
        </div>
      </li>
    </ul>
  </div>
</template>

    <script>
    import * as echarts from 'echarts'
    export default {
      name: 'PowerPredictionUI',
      mounted () {
        this.initShortTermChart()
        this.initUltraShortTermChart()
        this.initDailyLoadHeatmap()
        this.initModelRadarChart()
        this.MultiStationLoadChartinit()
        this.initGaugeChart()
      },
      methods: {
        initShortTermChart () {
          const chartDom = this.$refs.shortTermChart
          const myChart = echarts.init(chartDom)

          const option = {
            legend: {
          data: ['预测功率', '实际功率'],
          top: 'top',
          left: 'left',
          icon: 'rect',
          padding: 20,
          textStyle: {
            color: 'white'
          }
      },
            xAxis: {
              min: 0,
              max: 72,
              interval: 12,
              splitLine: { show: false, width: 1 },
  name: '(h)',
  nameTextStyle: { color: 'white' },
  axisLabel: { show: true, textStyle: { color: 'white', fontFamily: 'SimSun', fontWeight: 'bolder' } } },
            yAxis: {
               splitLine: { show: true, lineStyle: { type: 'solid', color: 'rgba(140,140,206,0.5)' } },
  axisLabel: { show: true, textStyle: { color: 'white', fontFamily: 'SimSun', fontWeight: 'bolder' } },
               min: -10.05,
               max: 90,
               interval: 14.20
              },
            grid:
            {
              show: true,
              borderColor: 'rgba(48,113,169,1)',
              borderWidth: 2
            },
            series: [{
              name: '实际功率',
              showSymbol: false,
              data: [ [0.0, 44.96], [0.73, 41.86], [1.45, 50.83], [2.18, 63.29], [2.91, 59.74], [3.64, 69.08], [4.36, 66.28], [5.09, 77.26], [5.82, 72.38], [6.55, 78.38],
  [7.27, 71.55], [8.0, 67.49], [8.73, 71.46], [9.45, 61.16], [10.18, 53.16], [10.91, 55.88], [11.64, 37.16], [12.36, 42.69], [13.09, 23.47], [13.82, 31.37],
  [14.55, 12.99], [15.27, 8.69], [16.0, 16.29], [16.73, 2.92], [17.45, 4.57], [18.18, 0.45], [18.91, 10.34], [19.64, 5.47], [20.36, 11.17], [21.09, 15.46],
  [21.82, 21.24], [22.55, 31.14], [23.27, 26.11], [24.0, 41.86], [24.73, 37.16], [25.45, 57.35], [26.18, 53.16], [26.91, 70.65], [27.64, 61.16], [28.36, 77.97],
  [29.09, 69.57], [29.82, 76.17], [30.55, 65.62], [31.27, 78.79], [32.0, 61.47], [32.73, 71.72], [33.45, 49.29], [34.18, 64.54], [34.91, 44.96], [35.64, 53.57],
  [36.36, 31.14], [37.09, 36.91], [37.82, 20.42], [38.55, 33.53], [39.27, 10.34], [40.0, 7.87], [40.73, 5.47], [41.45, 0.45], [42.18, 5.47], [42.91, -1.95],
  [43.64, 9.52], [44.36, 13.82], [45.09, 8.69], [45.82, 19.59], [46.55, 28.66], [47.27, 38.56], [48.0, 29.49], [48.73, 44.96], [49.45, 49.29], [50.18, 61.47],
  [50.91, 53.16], [51.64, 71.37], [52.36, 65.62], [53.09, 78.79], [53.82, 69.57], [54.55, 76.17], [55.27, 65.62], [56.0, 79.06], [56.73, 56.71], [57.45, 69.57],
  [58.18, 49.69], [58.91, 44.96], [59.64, 36.91], [60.36, 28.66], [61.09, 23.71], [61.82, 33.53], [62.55, 16.29], [63.27, 26.11], [64.0, 7.87], [64.73, 2.92],
  [65.45, 5.47], [66.18, 0.45], [66.91, 4.57], [67.64, 7.23], [68.36, 9.52], [69.09, 18.69], [69.82, 16.93], [70.55, 21.24], [71.27, 32.05], [72.0, 28.66]
  ],
              type: 'line',
              lineStyle: {
          normal: {
            color: '#ffc800',
            width: 1
          }
        },
        itemStyle: {
            color: '#ffc800'
          },
              smooth: false,
              markLine: {
              symbol: 'none',
              silent: true,
              lineStyle: {
                  color: 'rgba(140,140,206,0.9)',
                  type: 'solid'
              },
              label:
              {
                textStyle:
                { color: 'white', fontFamily: 'SimSun', fontWeight: 'bolder' }
              },
              data: [
                  { yAxis: 80.96,
                   name: 'Bottom Line'
                  }, // 最底部的线
                  { yAxis: -10.59,
                  name: 'Top Line'
                 } // 最顶部的线
              ]
          }
            },
            {
              name: '预测功率',
              showSymbol: false,
              data: [[0.0, 41.47], [0.73, 46.66], [1.45, 59.39], [2.18, 65.24], [2.91, 66.02], [3.64, 70.67], [4.36, 74.83], [5.09, 80.28], [5.82, 87.31], [6.55, 82.63],
  [7.27, 81.07], [8.0, 76.32], [8.73, 78.14], [9.45, 65.86], [10.18, 65.37], [10.91, 48.71], [11.64, 44.68], [12.36, 30.47], [13.09, 26.28], [13.82, 19.94],
  [14.55, 10.92], [15.27, -2.64], [16.0, -0.31], [16.73, -5.54], [17.45, -6.05], [18.18, -12.03], [18.91, -10.57], [19.64, -8.05], [20.36, -3.71], [21.09, 2.46],
  [21.82, 4.38], [22.55, 15.83], [23.27, 24.85], [24.0, 30.48], [24.73, 44.61], [25.45, 54.17], [26.18, 63.65], [26.91, 64.17], [27.64, 74.88], [28.36, 83.52],
  [29.09, 84.26], [29.82, 83.54], [30.55, 83.49], [31.27, 83.41], [32.0, 76.79], [32.73, 70.06], [33.45, 66.17], [34.18, 65.71], [34.91, 53.02], [35.64, 40.04],
  [36.36, 34.97], [37.09, 31.62], [37.82, 25.96], [38.55, 15.25], [39.27, 4.81], [40.0, -3.87], [40.73, -4.92], [41.45, -4.21], [42.18, -14.42], [42.91, -12.67],
  [43.64, -4.99], [44.36, -3.88], [45.09, -4.27], [45.82, 8.98], [46.55, 11.74], [47.27, 24.75], [48.0, 26.17], [48.73, 34.18], [49.45, 44.87], [50.18, 55.67],
  [50.91, 61.47], [51.64, 75.86], [52.36, 74.44], [53.09, 84.82], [53.82, 83.92], [54.55, 83.71], [55.27, 82.36], [56.0, 80.94], [56.73, 77.65], [57.45, 70.03],
  [58.18, 60.21], [58.91, 54.32], [59.64, 44.67], [60.36, 35.48], [61.09, 28.27], [61.82, 23.66], [62.55, 10.04], [63.27, 12.46], [64.0, 1.58], [64.73, -8.21],
  [65.45, -6.14], [66.18, -11.79], [66.91, -9.55], [67.64, -5.37], [68.36, -8.47], [69.09, 3.81], [69.82, 1.52], [70.55, 6.66], [71.27, 20.13], [72.0, 28.17]],
              type: 'line',
              lineStyle: {
          normal: {
            color: 'rgb(0, 255, 200) ',
            width: 1
          }
        },
        itemStyle: {
            color: 'rgb(0, 255, 200) '
          },
              smooth: true,
              markLine: {
              symbol: 'none',
              silent: true,
              lineStyle: {
                  color: 'rgba(140,140,206,0.9)',
                  type: 'solid'
              },
              label:
              {
                textStyle:
                { color: 'white', fontFamily: 'SimSun', fontWeight: 'bolder' }
              },
              data: [
                  { yAxis: 80.96,
                   name: 'Bottom Line'
                  }, // 最底部的线
                  { yAxis: -10.59,
                  name: 'Top Line'
                 } // 最顶部的线
              ]
          }
            }

          ]
          }
          myChart.setOption(option)
        },
        initUltraShortTermChart () {
          const chartDom = this.$refs.ultraShortTermChart
          const myChart = echarts.init(chartDom)
          const option = {
            legend: {
          data: ['预测功率', '实际功率'],
          top: 'top',
          left: 'left',
          icon: 'rect',
          padding: 20,
          textStyle: {
            color: 'white'
          }
      },
            grid:
            {
              show: true,
              borderColor: 'rgba(48,113,169,1)',
              borderWidth: 2
            },
            xAxis: { min: 0, max: 240, interval: 15, splitLine: { show: false, width: 1 }, name: '(min)', nameTextStyle: { color: 'white' }, axisLabel: { show: true, textStyle: { color: 'white', fontFamily: 'SimSun', fontWeight: 'bolder' } } },
            yAxis: { splitLine: { show: true, lineStyle: { type: 'solid', color: 'rgba(140,140,206,0.5)' } }, nameTextStyle: { color: 'white' }, axisLabel: { show: true, textStyle: { color: 'white', fontFamily: 'SimSun', fontWeight: 'bolder' } } },
            series: [
            {
              name: '实际功率',
              showSymbol: false,
              data: [[0, -2.61], [1, -1.67], [2, 2.52], [3, -2.12], [4, -2.38], [5, -5.22], [6, 1.49], [7, -6.35], [8, -0.80], [9, 1.02], [10, 2.62], [11, 0.12], [12, 1.61], [13, -5.16], [14, -5.20], [15, -5.37], [16, 1.98], [17, 2.27], [18, -6.69], [19, -6.94], [20, -2.52], [21, -2.56], [22, -1.77], [23, 1.71], [24, -5.34], [25, -2.71], [26, -6.35], [27, -3.13], [28, -6.40], [29, 2.04], [30, 3.25], [31, -3.91], [32, 2.02], [33, -2.49], [34, -2.60], [35, 2.19], [36, 2.04], [37, -3.91], [38, -3.87], [39, 3.01], [40, -2.51], [41, 1.74], [42, -2.99], [43, 0.73], [44, -5.06], [45, 2.35], [46, -6.90], [47, -3.79], [48, -3.16], [49, 0.94], [50, -4.33], [51, -3.19], [52, -1.91], [53, -6.30], [54, -1.07], [55, -4.93], [56, -5.28], [57, -1.67], [58, -3.17], [59, 1.29], [60, -1.46], [61, 2.79], [62, -1.64], [63, -0.03], [64, -5.71], [65, -6.09], [66, -2.14], [67, -5.00], [68, -1.15], [69, -5.79], [70, -1.26], [71, -0.78], [72, -0.62], [73, 1.36], [74, 0.35], [75, 7.47], [76, 5.29], [77, 12.62], [78, 12.34], [79, 22.43], [80, 26.16], [81, 21.07], [82, 16.46], [83, 24.95], [84, 38.70], [85, 25.52], [86, 27.18], [87, 48.98], [88, 39.77], [89, 34.58], [90, 27.83], [91, 50.47], [92, 46.49], [93, 38.85], [94, 57.12], [95, 74.11], [96, 67.30], [97, 75.87], [98, 88.63], [99, 71.90], [100, 89.62], [101, 88.18], [102, 82.85], [103, 77.85], [104, 97.75], [105, 59.11], [106, 73.27], [107, 59.51], [108, 79.37], [109, 80.29], [110, 77.00], [111, 62.20], [112, 82.28], [113, 50.21], [114, 84.43], [115, 51.67], [116, 105.45], [117, 94.28], [118, 55.24], [119, 90.67], [120, 75.17], [121, 102.27], [122, 83.31], [123, 53.82], [124, 55.69], [125, 54.66], [126, 88.39], [127, 83.30], [128, 104.36], [129, 50.73], [130, 44.24], [131, 96.09], [132, 79.14], [133, 51.33], [134, 36.14], [135, 44.09], [136, 21.28], [137, 69.71], [138, 72.32], [139, 70.10], [140, 76.25], [141, 64.74], [142, 35.51], [143, 34.07], [144, 13.32], [145, 60.72], [146, 60.66], [147, 13.64], [148, 35.42], [149, 24.36], [150, 31.03], [151, 22.34], [152, 19.67], [153, 16.46], [154, 12.02], [155, 6.63], [156, 5.50], [157, 6.81], [158, 3.62], [159, -2.52], [160, 0.75], [161, -0.79], [162, -3.40], [163, -0.51], [164, -5.04], [165, -3.75], [166, -4.59], [167, -2.51], [168, -3.84], [169, -4.86], [170, 0.41], [171, -1.35], [172, -7.58], [173, -1.85], [174, 0.88], [175, -3.20], [176, 0.60], [177, -1.14], [178, -0.95], [179, -1.29], [180, -1.12], [181, -5.37], [182, -2.73], [183, -6.96], [184, -6.28], [185, 0.14], [186, -1.80], [187, -4.67], [188, -4.36], [189, -5.81], [190, -5.11], [191, -5.12], [192, 1.57], [193, 1.50], [194, 1.68], [195, -2.02], [196, 1.52], [197, -5.41], [198, 0.47], [199, -1.54], [200, -4.25], [201, -2.15], [202, -0.93], [203, -0.99], [204, -1.47], [205, -1.40], [206, -1.58], [207, -1.89], [208, -5.62], [209, -5.82], [210, -5.65], [211, -5.94], [212, -1.77], [213, 2.43], [214, -3.33], [215, 1.96], [216, -1.32], [217, -6.81], [218, 0.98], [219, -6.59], [220, -4.84], [221, -0.78], [222, -3.16], [223, 2.04], [224, 2.43], [225, 0.87], [226, -2.88], [227, 2.08], [228, 0.18], [229, -5.75], [230, -4.29], [231, -3.89], [232, -4.07], [233, 1.64], [234, -7.00], [235, -1.26], [236, 2.05], [237, -2.55], [238, -5.34], [239, -4.92], [240, 1.51]],
              type: 'line',
              lineStyle: {
          normal: {
            color: '#ffc800',
            width: 1
          }

        },
        itemStyle: {
            color: '#ffc800'
          },
              smooth: false
            },
              {
              name: '预测功率',
              showSymbol: false,
              data: [[0, -1.95], [2, -1.87], [5, -2.15], [7, -2.32], [10, -2.05], [12, -1.78], [15, -1.92], [17, -2.25], [20, -2.45], [22, -2.15], [24, -1.85], [27, -1.68], [30, -1.75], [32, -2.10], [35, -1.95], [37, -1.65], [40, -1.82], [42, -2.18], [45, -2.35], [47, -2.05], [50, -1.75], [52, -1.85], [55, -2.20], [57, -2.45], [60, -2.25], [62, -1.95], [65, -1.68], [67, -1.85], [70, -2.10], [72, -1.90], [75, 5.25], [77, 10.85], [80, 18.45], [82, 25.65], [85, 32.80], [87, 39.45], [90, 45.75], [92, 52.40], [95, 58.65], [97, 64.20], [100, 69.80], [102, 74.35], [105, 78.65], [107, 81.25], [110, 82.85], [112, 83.10], [115, 82.75], [117, 81.45], [120, 79.85], [122, 77.25], [125, 74.65], [127, 71.20], [130, 67.45], [132, 63.25], [135, 58.75], [137, 53.45], [140, 47.85], [142, 41.65], [145, 35.25], [147, 28.85], [150, 22.45], [152, 16.25], [155, 10.15], [157, 4.25], [160, -0.45], [162, -1.35], [165, -1.75], [167, -1.85], [170, -2.45], [172, -2.75], [175, -2.25], [177, -1.85], [180, -1.45], [182, -1.95], [185, -2.65], [187, -2.85], [190, -2.35], [192, -1.85], [195, -1.45], [197, -1.95], [200, -2.55], [202, -2.85], [205, -2.35], [207, -1.75], [210, -1.25], [212, -1.85], [215, -2.45], [217, -2.85], [220, -2.35], [222, -1.75], [225, -1.35], [227, -1.85], [230, -2.45], [232, -2.75], [235, -2.25], [237, -1.65], [240, -1.85]],
              type: 'line',
              lineStyle: {
          normal: {
            color: 'rgb(0, 255, 200)',
            width: 1
          }
        },
        itemStyle: {
            color: 'rgb(0, 255, 200) '
          },
              smooth: true
            }
          ]
          }
          myChart.setOption(option)
        },
        initDailyLoadHeatmap () {
  const chartDom = this.$refs.dailyLoadHeatmap
  const myChart = echarts.init(chartDom)
  const hours = Array.from({ length: 24 }, (_, i) => `${i.toString().padStart(2, '0')}:00`)
  const days = ['5月3日', '5月4日', '5月5日', '5月6日', '5月7日', '5月8日', '5月9日']

  // 构造模拟数据：[x, y, value] => [hourIndex, dayIndex, loadValue]
  const data = []
  for (let day = 0; day < 7; day++) {
    for (let hour = 0; hour < 24; hour++) {
      const load = Math.floor(Math.random() * 1000) // 模拟负荷数据
      data.push([hour, day, load])
    }
  }

  const option = {
    tooltip: {
      position: 'top'
    },
    grid: {
      left: '10%',
      bottom: '10%',
      containLabel: true,
      show: true,
      borderColor: 'rgba(48,113,169,1)',
      borderWidth: 2
    },
    xAxis: {
      type: 'category',
      data: hours,
      splitArea: {
        show: true
      },
      name: '(小时)',
      nameTextStyle: { color: 'white' },
      axisLabel: {
        show: true,
        textStyle: {
          color: 'white',
          fontFamily: 'SimSun',
          fontWeight: 'bolder'
        }
      }
    },
    yAxis: {
      type: 'category',
      data: days,
      splitArea: {
        show: true
      },
      nameTextStyle: { color: 'white' },
      axisLabel: {
        show: true,
        textStyle: {
          color: 'white',
          fontFamily: 'SimSun',
          fontWeight: 'bolder'
        }
      }
    },
    visualMap: {
      min: 0,
      max: 1000,
      calculable: true,
      orient: 'horizontal',
      left: 'center',
      top: '2%',
      textStyle: {
        color: 'white'
      }
    },
    series: [{
      name: '负荷 (kW)',
      type: 'heatmap',
      data,
      label: {
        show: false
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
        },
        initModelRadarChart () {
  const chartDom = this.$refs.modelRadarChart
  const myChart = echarts.init(chartDom)
  const option = {
    tooltip: {},
    legend: {
      data: ['BLOOM', 'PaLM', 'LLaMA', 'CRM'],
      top: 'top',
      textStyle: {
        color: 'white'
      }
    },
    radar: {
      indicator: [
        { name: '准确率', max: 100 },
        { name: '召回率', max: 100 },
        { name: 'F1分数', max: 100 },
        { name: '推理速度', max: 100 },
        { name: '稳定性', max: 100 }
      ],
      splitLine: {
        lineStyle: {
          color: 'rgba(140,140,206,0.3)'
        }
      },
      axisLine: {
        lineStyle: {
          color: 'rgba(140,140,206,0.6)'
        }
      },
      splitArea: {
        show: true,
        areaStyle: {
          color: ['rgba(0,255,255,0.05)', 'rgba(0,255,255,0.02)']
        }
      }
    },
    series: [{
    center: ['50%', '70%'],

      name: '模型性能',
      type: 'radar',
      data: [
        {
          value: [78, 82, 80, 75, 85],
          name: 'BLOOM'
        },
        {
          value: [88, 85, 86, 70, 80],
          name: 'PaLM'
        },
        {
          value: [90, 89, 88, 60, 83],
          name: 'LLaMA'
        },
        {
          value: [85, 80, 82, 95, 90],
          name: 'CRM'
        }
      ],
      lineStyle: {
        width: 2
      }
    }]
  }

  myChart.setOption(option)
        },
        MultiStationLoadChartinit () {
  const chartDom = this.$refs.multiStationLoadChart
  const myChart = echarts.init(chartDom)

  const option = {
    tooltip: {
      trigger: 'axis'
    },
    legend: {
      data: ['北京', '杭州', '南昌'],
      top: 'top',
      textStyle: {
        color: 'white'
      }
    },
    grid: {
      left: '3%',
      right: '4%',
      bottom: '3%',
      containLabel: true,
      borderColor: 'rgba(48,113,169,1)',
      borderWidth: 2
    },
    xAxis: {
      type: 'category',
      boundaryGap: false,
      data: Array.from({ length: 24 }, (_, i) => `${i}:00`),
      axisLabel: {
        color: 'white'
      },
      axisLine: {
        lineStyle: {
          color: 'white'
        }
      }
    },
    yAxis: {
      type: 'value',
      name: '负荷(kW)',
      axisLabel: {
        color: 'white'
      },
      splitLine: {
        lineStyle: {
          color: 'rgba(140,140,206,0.5)'
        }
      },
      axisLine: {
        lineStyle: {
          color: 'white'
        }
      }
    },
    series: [
      {
        name: '北京',
        type: 'line',
        smooth: true,
        data: [120, 132, 101, 134, 90, 230, 210, 190, 180, 150, 130, 120, 145, 165, 175, 190, 200, 210, 220, 190, 160, 140, 130, 120],
        lineStyle: { color: '#00eaff' },
        itemStyle: { color: '#00eaff' },
        showSymbol: false
      },
      {
        name: '杭州',
        type: 'line',
        smooth: true,
        data: [100, 112, 95, 110, 80, 210, 180, 160, 170, 140, 120, 110, 130, 150, 165, 170, 180, 190, 200, 175, 150, 130, 110, 100],
        lineStyle: { color: '#ffc800' },
        itemStyle: { color: '#ffc800' },
        showSymbol: false
      },
      {
        name: '南昌',
        type: 'line',
        smooth: true,
        data: [90, 105, 85, 98, 70, 195, 170, 150, 140, 130, 110, 100, 120, 135, 150, 160, 170, 180, 190, 165, 140, 120, 100, 90],
        lineStyle: { color: '#ff4c4c' },
        itemStyle: { color: '#ff4c4c' },
        showSymbol: false
      }
    ]
  }

  myChart.setOption(option)
        },
        initGaugeChart () {
  const chartDom = this.$refs.gaugeChart
  const myChart = echarts.init(chartDom)

  const value = 76.5

  const option = {
    series: [
      {
        type: 'gauge',
        center: ['50%', '70%'],
        startAngle: 180,
        endAngle: 0,
        min: 0,
        max: 100,
        radius: '90%',
        splitNumber: 10,
        axisLine: {
          lineStyle: {
            width: 20,
            color: [
              [value / 100, new echarts.graphic.LinearGradient(0, 0, 1, 0, [
                { offset: 0, color: '#00c9e0' },
                { offset: 1, color: '#005fc1' }
              ])],
              [1, '#2e2e2e']
            ]
          }
        },
        pointer: {
          show: true,
          length: '70%',
          width: 6
        },
        progress: {
          show: true,
          width: 20,
          roundCap: true,
          itemStyle: {
            color: '#00c0ff'
          }
        },
        axisTick: {
          show: false
        },
        splitLine: {
          show: false
        },
        axisLabel: {
          distance: -45,
          color: '#fff',
          fontSize: 14
        },
        detail: {
          valueAnimation: true,
          fontSize: 36,
          fontWeight: 'bold',
          offsetCenter: [0, '20%'],
          color: '#00eaff',
          formatter: '{value} %'
        },
        data: [
          {
            value: value
          }
        ]
      }
    ]
  }

  myChart.setOption(option)
}
    }
  }
    </script>

    <style scoped>
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
  .header {
    display: flex;
    justify-content: space-between;
    background-color: #0a1d4d;
    color: rgb(27,243,248);
    padding: 10px;
    font-weight: bold;
    border-bottom: 2px solid #00aaff;
    font-size: 18px;
  }

  .header1 {
    font-size: 25px;
  }

  .header2 {
    margin-top: 6px;
  }

    .content {
      background-color: rgba(0, 0, 0, 0);
      display: grid;
      grid-template-columns: 7fr 3fr;
      gap: 20px;
      margin: 20px;
    }

  .section {
  position: relative;
  padding: 20px;
  color: #ffffff;
  font-family: Arial, sans-serif;
  overflow: hidden;
}
.head{position: relative; height: 90px;width: 1500px; background: url(../../assets/images/topbg.png) center bottom no-repeat; background-size:100% 100%;}
.head h1{  font-size: 30px;text-align: center; line-height: 90px; color: #daf9ff;}

.head .time{position: absolute; left: 40px; line-height: 40px; top: 0; opacity: .7}
.head .name{position: absolute; right:40px; line-height: 40px; top: 0;opacity: .7}
.tit{ display: flex; align-items: flex-end;color: white;}
.tit span{ background: url(../../assets/images/line1.png) no-repeat bottom right; font-size: 20px; white-space: nowrap; padding-bottom: 10px; padding-right: 20px;}
.tit p{ background: url(../../assets/images/line2.png) no-repeat bottom right; width: 100%; height: 13px; margin-bottom: 5px; opacity: .5}
.section .corner-br {
  bottom: 0;
  right: 0;
  border-top: none;
  border-left: none;
  border-bottom-right-radius: 6px;
}
  .chart {
    height: 300px;
    /* background-color:rgba(10, 29, 77, 0.3); */
    /* border: 1px solid #d9d9d9;  */
    border-radius: 5px; /* 图表圆角 */
    margin-top: 10px; /* 与标题的间距 */
    align-self: center;
  }

    .card-title {
      background-color: #1890ff;
      color: #ffffff;
      text-align: center;
      padding: 10px;
      border-top-left-radius: 6px;
      border-top-right-radius: 6px;
      font-size: large;
      font-weight: bold;
    }

    .stats-table {
      margin: 20px;
      width: 100%;
      border-collapse: collapse;
      margin-top: 10px;
    }
.nav1{margin-left: -20px; margin-right:-20px;}
.nav1>li{padding:0 20px; float: left;}

    .stats-table td {
      padding: 15px 20px;
      text-align: left;
      font-size: 18px;
      border: none;
    }
    .section-header {
    text-align: center;
    font-size: 18px;
    font-weight: bold;
    padding: 5px 0;
    border-bottom: 2px solid #00aaff; /* 标题下划线与右侧盒子统一 */
    margin-bottom: 10px;
    color: rgb(27,243,248); /* 标题颜色与右侧盒子统一 */
  }
  .clearfix:after, .clearfix:before {
    display: table;
    content: " ";
}
.clearfix:after {
    clear: both;
}
.box{  margin-bottom: 20px; position: relative;}
.mainbox{padding: 0px 20px;}
.map{position:absolute; z-index: 10; opacity: .8;top: 5%; width:60%; height: 100%; left: 20%;}

.map1,.map2,.map3{ position:absolute;  top:0; left: 0; width: 100%; height: 100%; display: flex; justify-content: center; align-items: center;}
.map1{ z-index: 2; animation: myfirst2 15s infinite linear; display: flex;}
.map2{ z-index: 3; opacity: 0.2; animation: myfirst 10s infinite linear;}
.map3{ z-index: 1;}
.map1 img{ width: 100%}
.map2 img{width: 82%}
.map3 img{width: 80%}
@keyframes myfirst2
{
from {transform: rotate(0deg);}
to {transform: rotate(359deg);}
}

@keyframes myfirst
{
from {transform: rotate(0deg);}
to {transform: rotate(-359deg);}
}
.boxnav{padding: 10px 0 ;}
.jcjg{height: 100%; margin-left: -10px; margin-right: -10px;}
.jcjg li{width: 33.33333%;height: 100%;  float: left; height: 100%; padding: 0 10px;}
.jcjg h3{background: url(../../assets/images/tit1.png) center right no-repeat; margin-bottom: 15px;  font-weight: normal; font-size: 15px;}
.jcnav{position: relative; background: url(../../assets/images/bg1.png) no-repeat left center; height: 160px; width: 100%;}
.jcnav2{ background: url(../../assets/images/bg2.png) no-repeat left center; height: 200px; }

.jcnav img{position: absolute; left:14px; top: 50%; margin-top: -24px; }
.jcnav2 img{ left:16px; margin-top: -30px; }
.jcnavp{padding-left:98px;}
.jcnavp>div{ border: 1px solid #1070aa; display: flex; font-size: 14px; align-items: center; padding: 5px 10px; margin-bottom: 26px; height: 36px;}
.jcnav2 .jcnavp>div{margin-bottom: 17px;}
.jcnavp>div ol{ white-space: nowrap;}
.jcnavp>div span{ padding-left:10px; color: #00e4ff; white-space: nowrap; }
.jcnavp>div i{font-size: 12px;padding-left: 5px;}

.fora{position: relative;}
.forb{position: absolute; width: 100%; left: 0; bottom: 0;}
.fora:before,.fora:after,.forb:before,.forb:after{position: absolute; content: ""; width:2px; height: 2px; border: 1px solid #00deff; opacity: .8;
box-shadow: 0 0 5px #00deff;}
.fora:before,.forb:before{left: -2px; top: -2px;}
.fora:after,.forb:after{right: -2px; top: -2px;}

.text-w{color: #ffe400}
.text-d{color: #ff0000}
.text-s{color: #14e144}
.text-b{color: #00deff}
    </style>
