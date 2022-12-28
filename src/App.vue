<template>
  <div class="container">
    <GlobalHeader :user="currentUser"></GlobalHeader>
    <!-- <ColumnList :list="list"></ColumnList> -->
    <ValidateForm @form-submit="onFormSubmit">
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">邮箱地址</label>
        <ValiadateInput :rules="emailRules" v-model="emailVal" placeholder="请输入邮箱地址" type="text"></ValiadateInput>
      </div>
      <div class="mb-3">
        <label for="exampleInputPassword1" class="form-label">密码</label>
        <ValiadateInput :rules="passwordRules" v-model="passwordVal" placeholder="请输入密码" type="password"></ValiadateInput>
      </div>
      <template #submit>
        <span class="btn btn-danger">提交</span>
      </template>
    </ValidateForm>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from './components/ColumnList.vue'
import ValiadateInput, { RulesProp } from './components/ValiadateInput.vue'
import ValidateForm from './components/ValidateForm.vue'
import GlobalHeader, { UserProps } from './components/GlobalHeader.vue'

const currentUser: UserProps = {
  isLogin: true,
  name: 'dashan'
}
const testData: ColumnProps[] = [
  {
    id: 1,
    title: 'test1的专栏',
    description: '这是的test1专栏，有一段非常有意思的简介，可以更新一下哦',
    avatar: 'http://wechatapppro-1252524126.file.myqcloud.com/apppcHqlTPT3482/image/compress/larger_YWxpdmVfY3JlYXRlQWxpdmVfN2Q2NDUzMDI.png'
  },
  {
    id: 2,
    title: 'test2的专栏',
    description: '这是的test2专栏，有一段非常有意思的简介，可以更新一下哦',
    avatar: 'http://wechatapppro-1252524126.file.myqcloud.com/app001idwxc5847/image/compress/640480550kkbxsya5083app2y1gq.jpg'
  },
  {
    id: 3,
    title: 'test3的专栏',
    description: '这是的test3专栏，有一段非常有意思的简介，可以更新一下哦,爱怎么说怎么说'
    // avatar: 'http://wechatapppro-1252524126.file.myqcloud.com/app001idwxc5847/image/compress/640480550kkbxsya5083app2y1gq.jpg'
  }
]
export default defineComponent({
  name: 'App',
  components: {
    // ColumnList,
    GlobalHeader,
    ValiadateInput,
    ValidateForm
  },
  setup () {
    const emailVal = ref('')
    const emailRules: RulesProp = [
      { type: 'required', message: '电子邮箱地址不能为空' },
      { type: 'email', message: '请输入正确的电子邮箱格式' }
    ]

    const passwordVal = ref('')
    const passwordRules: RulesProp = [
      { type: 'required', message: '密码不能为空' }
    ]

    const onFormSubmit = (result: boolean) => {
      console.log('1222', result)
    }

    return {
      list: testData,
      currentUser,
      emailRules,
      emailVal,
      passwordVal,
      passwordRules,
      onFormSubmit
    }
  }
})
</script>

<style>
</style>
