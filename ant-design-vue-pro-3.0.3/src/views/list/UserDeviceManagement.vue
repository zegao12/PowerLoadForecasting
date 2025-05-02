<template>
  <page-header-wrapper title="用户设备管理">
    <a-card :bordered="false">
      <!-- 搜索区域 -->
      <div class="table-page-search-wrapper">
        <a-form layout="inline">
          <a-row :gutter="48">
            <a-col :md="8" :sm="24">
              <a-form-item label="区域">
                <a-select v-model="queryParam.region" placeholder="全部区域">
                  <a-select-option value="">全部</a-select-option>
                  <a-select-option value="城区A">城区A</a-select-option>
                  <a-select-option value="工业区B">工业区B</a-select-option>
                  <a-select-option value="新区C">新区C</a-select-option>
                </a-select>
              </a-form-item>
            </a-col>
            <a-col :md="8" :sm="24">
              <a-form-item label="状态">
                <a-select v-model="queryParam.status" placeholder="全部状态">
                  <a-select-option value="">全部</a-select-option>
                  <a-select-option value="online">在线</a-select-option>
                  <a-select-option value="offline">离线</a-select-option>
                  <a-select-option value="deploying">部署中</a-select-option>
                </a-select>
              </a-form-item>
            </a-col>
            <a-col :md="8" :sm="24">
              <span class="table-page-search-submitButtons">
                <a-button type="primary" @click="handleSearch">查询</a-button>
                <a-button style="margin-left: 8px" @click="handleReset">重置</a-button>
              </span>
            </a-col>
          </a-row>
        </a-form>
      </div>

      <!-- 表格区域 -->
      <a-table
        :columns="columns"
        :dataSource="filteredData"
        :pagination="{ pageSize: 10 }"
        :rowKey="record => record.deviceId"
      >
        <template slot="action" slot-scope="record">
          <span class="action-wrapper">
            <a @click="viewLog(record)">查看日志</a>
            <a-divider type="vertical" />
            <a @click="redeploy(record)">重新部署</a>
          </span>
        </template>
      </a-table>
    </a-card>
  </page-header-wrapper>
</template>

  <script>
  export default {
    name: 'UserDeviceManagement',
    data () {
      return {
        queryParam: {
          region: '',
          status: ''
        },
        rawData: [
          { deviceId: 'A01', region: '城区A', modelVersion: 'S3TKFDL_v1.3', status: 'online', lastSync: '2025-04-30 10:15' },
          { deviceId: 'B02', region: '工业区B', modelVersion: 'S3TKFDL_v1.2', status: 'offline', lastSync: '2025-04-29 18:10' },
          { deviceId: 'C03', region: '新区C', modelVersion: 'S3TKFDL_v1.3', status: 'deploying', lastSync: '2025-04-30 09:50' },
          { deviceId: 'D04', region: '城区A', modelVersion: 'S3TKFDL_v1.1', status: 'online', lastSync: '2025-04-29 21:33' },
          { deviceId: 'E05', region: '工业区B', modelVersion: 'NoKFDL_v1.0', status: 'offline', lastSync: '2025-04-28 17:20' },
          { deviceId: 'F06', region: '新区C', modelVersion: 'S3TKFDL_v1.3', status: 'online', lastSync: '2025-04-30 08:10' },
          { deviceId: 'G07', region: '城区A', modelVersion: 'S3TKFDL_v1.3', status: 'deploying', lastSync: '2025-04-30 10:00' },
          { deviceId: 'H08', region: '工业区B', modelVersion: 'S3TKFDL_v1.2', status: 'online', lastSync: '2025-04-30 07:30' },
          { deviceId: 'I09', region: '新区C', modelVersion: 'NoDistill_v1.1', status: 'offline', lastSync: '2025-04-28 14:15' },
          { deviceId: 'J10', region: '城区A', modelVersion: 'S3TKFDL_v1.3', status: 'online', lastSync: '2025-04-30 10:12' }
        ],
        columns: [
          { title: '设备编号', dataIndex: 'deviceId', key: 'deviceId' },
          { title: '所属区域', dataIndex: 'region', key: 'region' },
          { title: '模型版本', dataIndex: 'modelVersion', key: 'modelVersion' },
          {
            title: '在线状态',
            dataIndex: 'status',
            key: 'status',
            customRender: (text) => {
              const map = {
                online: '✅ 在线',
                offline: '❌ 离线',
                deploying: '⏳ 部署中'
              }
              return map[text] || '未知'
            }
          },
          { title: '最后同步时间', dataIndex: 'lastSync', key: 'lastSync' },
          {
            title: '操作',
            key: 'action',
            scopedSlots: { customRender: 'action' }
          }
        ]
      }
    },
    computed: {
      filteredData () {
        return this.rawData.filter(item => {
          const matchRegion = !this.queryParam.region || item.region === this.queryParam.region
          const matchStatus = !this.queryParam.status || item.status === this.queryParam.status
          return matchRegion && matchStatus
        })
      }
    },
    methods: {
      handleSearch () {
        // 过滤通过 computed 完成，无需刷新
      },
      handleReset () {
        this.queryParam = { region: '', status: '' }
      },
      viewLog (record) {
        this.$message.info(`查看日志：${record.deviceId}`)
      },
      redeploy (record) {
        this.$message.success(`已重新部署设备 ${record.deviceId}`)
      }
    }
  }
  </script>

  <style scoped>
  .table-page-search-wrapper {
    margin-bottom: 20px;
  }
  .action-wrapper {
    display: inline-flex;
    align-items: center;
  }
  </style>
