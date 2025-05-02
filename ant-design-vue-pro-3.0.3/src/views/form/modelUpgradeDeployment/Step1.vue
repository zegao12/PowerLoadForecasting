<template>
  <div>
    <a-form :form="form" style="max-width: 600px; margin: 40px auto 0;">
      <a-form-item label="模型版本" :labelCol="labelCol" :wrapperCol="wrapperCol">
        <a-select
          placeholder="请选择模型版本"
          v-decorator="['modelVersion', { rules: [{ required: true, message: '模型版本必须填写' }] }]">
          <a-select-option value="S3TKFDL_v1.3">S3TKFDL_v1.3</a-select-option>
          <a-select-option value="S3TKFDL_v1.2">S3TKFDL_v1.2</a-select-option>
        </a-select>
      </a-form-item>

      <a-form-item label="模型结构类型" :labelCol="labelCol" :wrapperCol="wrapperCol">
        <a-select
          placeholder="请选择模型结构"
          v-decorator="['modelType', { rules: [{ required: true, message: '模型结构类型必须填写' }] }]">
          <a-select-option value="S3TKFDL">S3TKFDL</a-select-option>
          <a-select-option value="NoS3T">变体1（无时空模块）</a-select-option>
          <a-select-option value="NoKFDL">变体2（无联邦蒸馏）</a-select-option>
          <a-select-option value="NoDistill">变体3（无知识蒸馏）</a-select-option>
        </a-select>
      </a-form-item>

      <a-form-item label="启用知识蒸馏" :labelCol="labelCol" :wrapperCol="wrapperCol">
        <a-switch v-decorator="['enableDistill', { valuePropName: 'checked', initialValue: true }]" />
      </a-form-item>

      <a-form-item label="KNN最近邻K值" :labelCol="labelCol" :wrapperCol="wrapperCol">
        <a-input-number
          :min="1"
          :max="10"
          v-decorator="['knnK', { initialValue: 3, rules: [{ required: true, message: '请输入K值' }] }]"
          style="width: 100%" />
      </a-form-item>

      <a-form-item label="蒸馏权重α" :labelCol="labelCol" :wrapperCol="wrapperCol">
        <a-input-number
          :min="0"
          :max="1"
          :step="0.1"
          v-decorator="['alpha', { initialValue: 0.5, rules: [{ required: true, message: '请输入α值' }] }]"
          style="width: 100%" />
      </a-form-item>

      <a-form-item label="本地预训练轮数" :labelCol="labelCol" :wrapperCol="wrapperCol">
        <a-input-number
          :min="1"
          :max="20"
          v-decorator="['localRounds', { initialValue: 5, rules: [{ required: true }] }]"
          style="width: 100%" />
      </a-form-item>

      <a-form-item label="操作员姓名" :labelCol="labelCol" :wrapperCol="wrapperCol">
        <a-input v-decorator="['operator', { initialValue: 'Alex', rules: [{ required: true, message: '操作员姓名必须填写' }] }]" />
      </a-form-item>

      <a-form-item label="操作备注" :labelCol="labelCol" :wrapperCol="wrapperCol">
        <a-input
          placeholder="如：手动部署S3TKFDL_v1.3"
          v-decorator="['note', { rules: [{ required: true, message: '备注必填' }] }]" />
      </a-form-item>

      <a-form-item :wrapperCol="{ span: 19, offset: 5 }">
        <a-button type="primary" @click="nextStep">下一步</a-button>
      </a-form-item>
    </a-form>

    <a-divider />

    <div class="step-form-style-desc">
      <h3>说明</h3>
      <p>本页面用于配置模型升级参数并准备部署至边缘设备。</p>
      <p>使用KNN蒸馏时，中央服务器将选取K个最相似设备模型构建教师模型。</p>
      <p>蒸馏位置：固定为解码器。</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModelDeployStep1',
  data () {
    return {
      labelCol: { lg: { span: 5 }, sm: { span: 5 } },
      wrapperCol: { lg: { span: 19 }, sm: { span: 19 } },
      form: this.$form.createForm(this)
    }
  },
  methods: {
    nextStep () {
      this.form.validateFields((err, values) => {
        if (!err) {
          this.$emit('nextStep', values) // 将配置值传递到下一步或父组件
        }
      })
    }
  }
}
</script>

<style lang="less" scoped>
.step-form-style-desc {
  padding: 0 56px;
  color: rgba(0, 0, 0, .45);

  h3 {
    margin-bottom: 12px;
    font-size: 16px;
    color: rgba(0, 0, 0, .65);
  }

  p {
    margin-bottom: 8px;
    line-height: 22px;
  }
}
</style>
