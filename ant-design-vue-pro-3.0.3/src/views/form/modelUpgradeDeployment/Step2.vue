<template>
  <div>
    <a-form :form="form" style="max-width: 600px; margin: 40px auto 0;">
      <a-alert
        :closable="true"
        message="确认部署后，模型将推送至边缘设备，过程不可撤回。"
        type="warning"
        style="margin-bottom: 24px;"
      />

      <!-- 只读信息 -->
      <a-form-item label="模型版本" :labelCol="labelCol" :wrapperCol="wrapperCol" class="stepFormText">
        {{ config.modelVersion }}
      </a-form-item>
      <a-form-item label="模型结构" :labelCol="labelCol" :wrapperCol="wrapperCol" class="stepFormText">
        {{ config.modelType }}
      </a-form-item>
      <a-form-item label="启用知识蒸馏" :labelCol="labelCol" :wrapperCol="wrapperCol" class="stepFormText">
        {{ config.enableDistill ? '是' : '否' }}
      </a-form-item>
      <a-form-item label="K值" :labelCol="labelCol" :wrapperCol="wrapperCol" class="stepFormText">
        {{ config.knnK }}
      </a-form-item>
      <a-form-item label="蒸馏参数 α" :labelCol="labelCol" :wrapperCol="wrapperCol" class="stepFormText">
        {{ config.alpha }}
      </a-form-item>
      <a-form-item label="部署设备数" :labelCol="labelCol" :wrapperCol="wrapperCol" class="stepFormText">
        {{ config.deviceCount }} 台
      </a-form-item>

      <a-divider />

      <!-- 输入项 -->
      <a-form-item label="管理员密码" :labelCol="labelCol" :wrapperCol="wrapperCol">
        <a-input
          type="password"
          placeholder="请输入确认密码"
          style="width: 80%;"
          v-decorator="['adminPassword', {
            rules: [{ required: true, message: '请输入管理员密码' }]
          }]"
        />
      </a-form-item>

      <a-form-item :wrapperCol="{ span: 19, offset: 5 }">
        <a-button :loading="loading" type="primary" @click="submitDeploy">确认部署</a-button>
        <a-button style="margin-left: 8px" @click="prevStep">上一步</a-button>
      </a-form-item>
    </a-form>
  </div>
</template>

<script>
export default {
  name: 'DeployStep2',
  props: {
    config: {
      type: Object,
      default: () => ({
        modelVersion: 'S3TKFDL_v1.3',
        modelType: 'S3TKFDL',
        enableDistill: true,
        knnK: 3,
        alpha: 0.5,
        deviceCount: 10
      })
    }
  },
  data () {
    return {
      form: this.$form.createForm(this),
      labelCol: { lg: { span: 5 }, sm: { span: 5 } },
      wrapperCol: { lg: { span: 19 }, sm: { span: 19 } },
      loading: false,
      timer: 0
    }
  },
  methods: {
    submitDeploy () {
      this.loading = true
      this.form.validateFields((err, values) => {
        if (!err) {
          console.log('提交部署：', values, this.config)
          this.timer = setTimeout(() => {
            this.loading = false
            this.$emit('nextStep', { ...this.config, ...values })
          }, 1500)
        } else {
          this.loading = false
        }
      })
    },
    prevStep () {
      this.$emit('prevStep')
    }
  },
  beforeDestroy () {
    clearTimeout(this.timer)
  }
}
</script>

<style lang="less" scoped>
.stepFormText {
  margin-bottom: 24px;

  .ant-form-item-label,
  .ant-form-item-control {
    line-height: 22px;
  }
}
</style>
