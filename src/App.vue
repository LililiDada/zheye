<template>
  <div class="container">
    <GlobalHeader :user="currentUser"></GlobalHeader>
    <!-- <ColumnList :list="list"></ColumnList> -->
    <form action="">
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">邮箱地址</label>
        <ValiadateInput :rules="emailRules" v-model="emailVal"></ValiadateInput>
      </div>
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">邮箱地址</label>
        <input type="email" class="form-control" id="exampleInputEmail1" v-model="emailRef.val" @blur="validateEmail">
        <div class="form-text" v-if="emailRef.error">{{ emailRef.message }}</div>
      </div>
      <div class="mb-3">
        <label for="exampleInputPassword1" class="form-label">密码</label>
        <input type="password" class="form-control" id="exampleInputPassword1">
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from './components/ColumnList.vue'
import ValiadateInput, { RulesProp } from './components/ValiadateInput.vue'
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
const emailReg = /^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/
export default defineComponent({
  name: 'App',
  components: {
    // ColumnList,
    GlobalHeader,
    ValiadateInput
  },
  setup () {
    const emailVal = ref('dashan')

    const emailRules: RulesProp = [
      { type: 'required', message: '电子邮箱地址不能为空' },
      { type: 'email', message: '请输入正确的电子邮箱格式' }
    ]

    const emailRef = reactive({
      val: '',
      error: false,
      message: ''
    })

    const validateEmail = () => {
      if (emailRef.val.trim() === '') {
        emailRef.error = true
        emailRef.message = 'can not be empty'
      } else if (!emailReg.test(emailRef.val)) {
        emailRef.error = true
        emailRef.message = 'should be vaild email'
      }
    }
    return {
      list: testData,
      currentUser,
      emailRef,
      validateEmail,
      emailRules,
      emailVal
    }
  }
})
</script>

<style>
</style>
