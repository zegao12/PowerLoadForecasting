<template>
  <page-header-wrapper title="系统评估日志">
    <a-card :bordered="false">
      <div class="table-page-search-wrapper" style="padding: 0">
        <a-form layout="inline" :label-col="{ span: 6 }" :wrapper-col="{ span: 18 }">
          <a-row :gutter="16">
            <a-col :md="8" :sm="24">
              <a-form-item label="模型版本" style="margin-bottom: 12px">
                <a-select v-model="queryParam.modelVersion" placeholder="请选择" style="width: 100%">
                  <a-select-option value="S3TKFDL_v1.3">S3TKFDL_v1.3</a-select-option>
                  <a-select-option value="S3TKFDL_v1.2">S3TKFDL_v1.2</a-select-option>
                  <a-select-option value="S3TKFDL_v1.1">S3TKFDL_v1.1</a-select-option>
                </a-select>
              </a-form-item>
            </a-col>
            <a-col :md="8" :sm="24">
              <a-form-item label="数据集" style="margin-bottom: 12px">
                <a-select v-model="queryParam.dataset" placeholder="请选择" style="width: 100%">
                  <a-select-option value="GEFCom2012">GEFCom2012</a-select-option>
                  <a-select-option value="GEFCom2017">GEFCom2017</a-select-option>
                </a-select>
              </a-form-item>
            </a-col>
            <a-col :md="8" :sm="24">
              <a-form-item label="区域数" style="margin-bottom: 12px">
                <a-select v-model="queryParam.regionCount" placeholder="请选择" style="width: 100%">
                  <a-select-option value="10">10</a-select-option>
                  <a-select-option value="20">20</a-select-option>
                  <a-select-option value="60">60</a-select-option>
                </a-select>
              </a-form-item>
            </a-col>
          </a-row>
          <a-row :gutter="16">
            <a-col :md="8" :sm="24">
              <a-form-item label="预测窗口" style="margin-bottom: 12px">
                <a-select v-model="queryParam.predictWindow" placeholder="请选择" style="width: 100%">
                  <a-select-option value="3h">3小时</a-select-option>
                  <a-select-option value="7h">7小时</a-select-option>
                  <a-select-option value="12h">12小时</a-select-option>
                </a-select>
              </a-form-item>
            </a-col>
            <a-col :md="8" :sm="24">
              <a-form-item label="评估指标" style="margin-bottom: 12px">
                <a-select v-model="queryParam.metric" placeholder="请选择" style="width: 100%">
                  <a-select-option value="MAE">MAE</a-select-option>
                  <a-select-option value="RMSE">RMSE</a-select-option>
                  <a-select-option value="MAPE">MAPE</a-select-option>
                </a-select>
              </a-form-item>
            </a-col>
            <a-col :md="8" :sm="24">
              <a-form-item label="时间范围" style="margin-bottom: 12px">
                <a-range-picker
                  v-model="queryParam.dateRange"
                  style="width: 100%"
                  :placeholder="['开始', '结束']"
                />
              </a-form-item>
            </a-col>
          </a-row>
          <a-row>
            <a-col :span="24" style="text-align: right; padding-top: 0">
              <a-button type="primary" @click="handleSearch">查询</a-button>
              <a-button style="margin-left: 8px" @click="handleReset">重置</a-button>
            </a-col>
          </a-row>
        </a-form>
      </div>

      <s-table
        :columns="columns"
        :data="loadData"
        :pagination="true"
        rowKey="id"
      />
    </a-card>
  </page-header-wrapper>
</template>

  <script>
  import { STable } from '@/components'

  const columns = [
    { title: '评估时间', dataIndex: 'date', sorter: true },
    { title: '模型版本', dataIndex: 'modelVersion' },
    { title: '数据集', dataIndex: 'dataset' },
    { title: '区域数', dataIndex: 'regionCount' },
    { title: '预测窗口', dataIndex: 'predictWindow' },
    { title: 'MAE', dataIndex: 'mae' },
    { title: 'RMSE', dataIndex: 'rmse' },
    { title: 'MAPE', dataIndex: 'mape' },
    { title: '操作人', dataIndex: 'operator' }
  ]

  export default {
    name: 'EvalLogTable',
    components: {
      STable
    },
    data () {
      return {
        columns,
        queryParam: {
          modelVersion: '',
          startTime: '',
          endTime: ''
        },
        loadData: parameter => {
          const requestParameters = Object.assign({}, parameter, this.queryParam)
          console.log('请求参数:', requestParameters)
          return this.getMockEvalLogs(requestParameters)
        }
      }
    },
    methods: {
  getMockEvalLogs () {
    // 增加10条假数据
    const data = [
      {
        id: '1',
        date: '2025-04-30 10:25',
        modelVersion: 'S3TKFDL_v1.3',
        dataset: 'GEFCom2012',
        regionCount: 20,
        predictWindow: '3h',
        mae: 2985,
        rmse: 5261,
        mape: '2.41%',
        operator: 'Alex'
      },
      {
        id: '2',
        date: '2025-04-29 09:15',
        modelVersion: 'S3TKFDL_v1.2',
        dataset: 'GEFCom2017',
        regionCount: 60,
        predictWindow: '12h',
        mae: 477,
        rmse: 1064,
        mape: '1.05%',
        operator: 'Jamie'
      },
      {
        id: '3',
        date: '2025-04-28 08:10',
        modelVersion: 'S3TKFDL_v1.1',
        dataset: 'GEFCom2012',
        regionCount: 30,
        predictWindow: '6h',
        mae: 1200,
        rmse: 2300,
        mape: '3.15%',
        operator: 'Chris'
      },
      {
        id: '4',
        date: '2025-04-27 14:40',
        modelVersion: 'S3TKFDL_v1.0',
        dataset: 'GEFCom2017',
        regionCount: 40,
        predictWindow: '8h',
        mae: 800,
        rmse: 1500,
        mape: '4.20%',
        operator: 'Patricia'
      },
      {
        id: '5',
        date: '2025-04-26 12:00',
        modelVersion: 'S3TKFDL_v1.2',
        dataset: 'GEFCom2012',
        regionCount: 50,
        predictWindow: '10h',
        mae: 1050,
        rmse: 1900,
        mape: '2.80%',
        operator: 'Jordan'
      },
      {
        id: '6',
        date: '2025-04-25 16:30',
        modelVersion: 'S3TKFDL_v1.3',
        dataset: 'GEFCom2017',
        regionCount: 25,
        predictWindow: '5h',
        mae: 320,
        rmse: 540,
        mape: '1.60%',
        operator: 'Morgan'
      },
      {
        id: '7',
        date: '2025-04-24 11:50',
        modelVersion: 'S3TKFDL_v1.1',
        dataset: 'GEFCom2012',
        regionCount: 45,
        predictWindow: '9h',
        mae: 450,
        rmse: 950,
        mape: '2.20%',
        operator: 'Taylor'
      },
      {
        id: '8',
        date: '2025-04-23 13:40',
        modelVersion: 'S3TKFDL_v1.0',
        dataset: 'GEFCom2017',
        regionCount: 35,
        predictWindow: '7h',
        mae: 620,
        rmse: 1100,
        mape: '1.95%',
        operator: 'Morgan'
      },
      {
        id: '9',
        date: '2025-04-22 10:55',
        modelVersion: 'S3TKFDL_v1.2',
        dataset: 'GEFCom2012',
        regionCount: 55,
        predictWindow: '8h',
        mae: 950,
        rmse: 1600,
        mape: '2.10%',
        operator: 'Alex'
      },
      {
        id: '10',
        date: '2025-04-21 15:30',
        modelVersion: 'S3TKFDL_v1.3',
        dataset: 'GEFCom2017',
        regionCount: 70,
        predictWindow: '10h',
        mae: 1400,
        rmse: 2200,
        mape: '3.30%',
        operator: 'Jamie'
      }
    ]
    return Promise.resolve({
      data,
      total: data.length,
      pageSize: 10,
      current: 1
    })
  }
}
  }
  </script>
