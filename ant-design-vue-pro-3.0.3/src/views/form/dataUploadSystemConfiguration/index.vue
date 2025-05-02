<template>
  <page-header-wrapper title="发起预测任务" content="选择模型，配置参数，并上传数据发起短期电力负荷预测">
    <a-card :body-style="{ padding: '24px 32px' }" :bordered="false">
      <a-form @submit="handleSubmit" :form="form">

        <!-- 模型版本选择 -->
        <a-form-item label="模型版本" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-select v-decorator="['modelVersion', { rules: [{ required: true, message: '请选择模型版本' }] }]">
            <a-select-option value="S3TKFDL_v1.3">S3TKFDL_v1.3</a-select-option>
            <a-select-option value="S3TKFDL_v1.2">S3TKFDL_v1.2</a-select-option>
          </a-select>
        </a-form-item>

        <!-- 是否启用知识蒸馏 -->
        <a-form-item label="是否启用知识蒸馏" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-radio-group v-model="queryParam.enableDistill" v-decorator="['enableDistill', { initialValue: true }]">
            <a-radio :value="true">是</a-radio>
            <a-radio :value="false">否</a-radio>
          </a-radio-group>
        </a-form-item>

        <!-- 蒸馏参数 -->
        <a-form-item label="KNN最近邻K值" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-input-number :min="1" :max="10" v-decorator="['knnK', { initialValue: 3 }]" />
        </a-form-item>

        <a-form-item label="蒸馏权重 α" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-input-number :min="0" :max="1" :step="0.1" v-decorator="['alpha', { initialValue: 0.5 }]" />
        </a-form-item>

        <!-- 上传数据 -->
        <a-form-item label="上传历史负荷数据" :labelCol="labelCol" :wrapperCol="wrapperCol">
          <a-upload
            name="file"
            :action="uploadAction"
            :before-upload="beforeUpload"
            :file-list="fileList"
            :showUploadList="true"
          >
            <a-button type="primary">
              <a-icon type="upload" />
              上传CSV文件
            </a-button>
          </a-upload>
        </a-form-item>

        <!-- 操作按钮 -->
        <a-form-item :wrapperCol="{ span: 24 }" style="text-align: center">
          <a-button htmlType="submit" type="primary" @click="showUploadComponent = true">提交配置</a-button>
          <a-button style="margin-left: 8px" @click="handlePredict">立即预测</a-button>
        </a-form-item>
      </a-form>
    </a-card>
  </page-header-wrapper>
</template>

<script>
import { Form, message, Upload, Icon } from 'ant-design-vue'

export default {
  name: 'LoadForecastForm',
  components: {
    'a-upload': Upload,
    'a-icon': Icon
  },
  data () {
    return {
      form: Form.createForm(this),
      queryParam: {
        enableDistill: true
      },
      fileList: [],
      uploadAction: '/api/predict/upload', // 替换为后端真实接口
      showUploadComponent: false
    }
  },
  methods: {
    handleSubmit (e) {
      e.preventDefault()
      this.form.validateFields((err, values) => {
        if (!err) {
          console.log('提交参数：', values)
          message.success('配置已提交')
        }
      })
    },
    handlePredict () {
      message.success('已发起预测任务')
    },
    beforeUpload (file) {
      this.fileList = [...this.fileList, file]
      return false // 阻止自动上传，交由 handleSubmit 控制
    }
  },
  computed: {
    labelCol () {
      return { lg: { span: 7 }, sm: { span: 7 } }
    },
    wrapperCol () {
      return { lg: { span: 10 }, sm: { span: 17 } }
    }
  }
}
</script>

<style scoped>
</style>
