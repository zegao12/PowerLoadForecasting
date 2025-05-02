<template>
  <div>
    <a-form>
      <a-result
        title="模型部署成功"
        :is-success="true"
        sub-title="部署已完成，边缘设备将自动同步模型参数"
        style="max-width: 600px; margin: 40px auto 0;"
      >
        <div class="information">
          <a-row>
            <a-col :sm="8" :xs="24">模型版本：</a-col>
            <a-col :sm="16" :xs="24">{{ config.modelVersion }}</a-col>
          </a-row>
          <a-row>
            <a-col :sm="8" :xs="24">模型结构：</a-col>
            <a-col :sm="16" :xs="24">{{ config.modelType }}</a-col>
          </a-row>
          <a-row>
            <a-col :sm="8" :xs="24">启用知识蒸馏：</a-col>
            <a-col :sm="16" :xs="24">{{ config.enableDistill ? '是' : '否' }}</a-col>
          </a-row>
          <a-row>
            <a-col :sm="8" :xs="24">K值：</a-col>
            <a-col :sm="16" :xs="24">{{ config.knnK }}</a-col>
          </a-row>
          <a-row>
            <a-col :sm="8" :xs="24">蒸馏参数 α：</a-col>
            <a-col :sm="16" :xs="24">{{ config.alpha }}</a-col>
          </a-row>
          <a-row>
            <a-col :sm="8" :xs="24">部署设备：</a-col>
            <a-col :sm="16" :xs="24">
              <span class="success">{{ config.deploySuccess }}</span> /
              <span class="total">{{ config.deviceCount }}</span> 台成功
            </a-col>
          </a-row>
          <a-row>
            <a-col :sm="8" :xs="24">操作员：</a-col>
            <a-col :sm="16" :xs="24">{{ config.operator }}</a-col>
          </a-row>
        </div>
        <template #extra>
          <a-button type="primary" @click="finish">返回首页</a-button>
          <a-button style="margin-left: 8px" @click="viewDevices">查看设备状态</a-button>
        </template>
      </a-result>
    </a-form>
  </div>
</template>

<script>
export default {
  name: 'DeployStep3',
  props: {
    config: {
      type: Object,
      default: () => ({
        modelVersion: 'S3TKFDL_v1.3',
        modelType: 'S3TKFDL',
        enableDistill: true,
        knnK: 3,
        alpha: 0.5,
        deploySuccess: 14,
        deviceCount: 15,
        operator: 'Alex'
      })
    }
  },
  methods: {
    finish () {
      this.$emit('finish')
    },
    viewDevices () {
      this.$router.push('/device/manage')
    }
  }
}
</script>

<style lang="less" scoped>
.information {
  line-height: 22px;

  .ant-row:not(:last-child) {
    margin-bottom: 20px;
  }
}
.success {
  color: #52c41a;
  font-weight: bold;
}
.total {
  font-weight: bold;
}
</style>
