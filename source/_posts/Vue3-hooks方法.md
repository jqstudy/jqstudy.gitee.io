---
title: Vue3-hooks方法
date: 2023-09-16 09:10:10
tags:
categories: web前端
---

### 1. hooks定义

一些可复用的方法像钩子一样挂着，可以随时被引入和调用以实现高内聚低耦合的目标，应该都能算是hook

### 2. 为什么Vue3要用自定义Hook？

结论：就是为了让Compoosition Api更好用更丰满，让写Vue3更畅快！像写诗一样写代码！
其实这个问题更深意义是为什么Vue3比Vue2更好！无外呼性能大幅度提升，其实编码体验也是Vue3的优点**Composition Api的引入（解决Option Api在代码量大的情况下的强耦合）** 让开发者有更好的开发体验。
个人碎碎念：但是这些所谓的提高开发体验都是需要开发者不断学习养成编码好习惯

### 3. 定义表格请求 hooks uselist

#### 3.1 js版

```javascript
import { ref } from 'vue'
import { ElMessage } from 'element-plus'

/**
 * 获取数据操作
 * @param { Function } api 请求的方法 required
 * @param { params } page
 * @param { params } size
 * @param { params } isAuto 是否是分页请求
 * @param { params } key  返回数据的键值
 * @param { callback } cb
 * @return { Object } { page,size,total,showSearch,loading,query,tableData,getList,reset }
*/
export function useList(api, params, cb) {
  if(!api) throw new Error('api is not found')
  const page = ref(params.page || 1)
  const size = ref(params.size || 10)
  const total = ref(0)
  const query = ref({})
  const loading = ref(false)
  const showSearch = ref(true)
  const isAuto = ref(params.isAuto || true)
  const tableData = ref([])
  const key = params.key || 'rows'

  function getList(obj = {}) {
    if(!loading.value) {
      loading.value = true
      const defaultParams = params.params || {}
      const data = isAuto.value ? Object.assign(obj, { pageNum: page.value, pageSize: size.vlaue }, query.value, defaultParams) : Object.assign(obj, query.value, defaultParams)
      const res = api(data).then(res => {
        loading.value = false
        tableData.value = cb ? cb(res[key]) : res[key]
        total.value = res.total || 0
      }).catch(c => {
        loading.value = false
        ElMessage.error(c)
      })
    }
  }

  function reset() {
    query.value = {}
    getList()
  }

  return {
    page,
    size,
    total,
    query,
    loading,
    showSearch,
    tableData,
    getList,
    reset
  }
}
```

#### 3.2 ts版

```typescript
import { ref, Ref } from 'vue'
import { ElMessage } from 'element-plus'

interface resultData<T> {
  code: number
  rows?: Array<T>
  data: Array<T>
  total?: number
  msg: string
}

interface paramsFace {
  page?: number
  size?: number
  isAuto?: boolean
  key?: string
  params?: any
}

interface resultFn<searchForm, tableForm> {
  page: Ref<number>
  size: Ref<number>
  total: Ref<number>
  loading: Ref<boolean>
  showSearch: Ref<boolean>
  query: Ref<searchForm>
  tableData: Ref<tableForm[]>
  getList: Function
  reset: Function
}

/**
 * 获取数据操作
 * @param { Function } api 请求的方法 required
 * @param { paramsFace } params
 * @param { callback } cb
 * @return { resultFn } { page,size,total,loading,query,tableData,getList,reset }
*/
export function useList<searchForm, tableForm>(api: Function, params: paramsFace, cb: Function): resultFn {
  if(!api) throw new Error('api is not found')
  const page = ref<number>(params.page || 1)
  const size = ref<number>(params.size || 10)
  const total = ref<number>(0)
  const query = ref<searchForm>({})
  const loading = ref<boolean>(false)
  const showSearch = ref<boolean>(true)
  const isAuto = ref<boolean>(params.isAuto || true)
  const tableData = ref<tableForm[]>([])
  const key: string = params.key || 'rows'

  function getList(obj = {}) {
    if(!loading.value) {
      loading.value = true
      const defaultParams: searchForm = params.params || {}
      const data = isAuto.value ? Object.assign(obj, { pageNum: page.value, pageSize: size.vlaue }, query.value, defaultParams) : Object.assign(obj, query.value, defaultParams)
      api(data).then((res: resultData<tableForm>) => {
        loading.value = false
        tableData.value = cb ? cb(res[key]) : res[key]
        total.value = res.total || 0
      }).catch(c => {
        loading.value = false
        ElMessage.error(c)
      })
    }
  }

  function reset() {
    query.value = {}
    getList()
  }

  return {
    page,
    size,
    total,
    query,
    loading,
    showSearch,
    tableData,
    getList,
    reset
  }
}
```

### 4. 弹窗 useModal

#### 4.1 js版

```javascript
import { ref, Ref, computed } from 'vue'

/**
 * 弹窗操作
 * @param { params } defaultForm 默认参数
 * @param { params } add 
 * @param { params } edit 
 * @return { Object } {
 *  visible,
    isTitle,
    modalForm,
    modalFormRefs,
    title,
    open,
    close,
    submit
    }
*/
export function useModal(params) {
  const visible = ref(false)
  const isTitle = ref(true)
  const modalForm = ref(params.defaultForm || {})
  const modalFormRefs = ref(null)
  const title = computed(() => isTitle.value ? '添加' : '修改')
  
  function open() {
    visible.value = true
  }

  function close() {
    visible.value = false
    isTitle.value = true
    modalForm.value = params.defaultForm || {}
    modalFormRefs.value && modalFormRefs.value.resetFields()
  }

  function submit() {
    modalFormRefs.value && modalFormRefs.value.validate(valid => {
      if(!valid) return
      isTitle.value ? params.add(modalForm.value) : params.edit(modalForm.value)
    })
  }

  return {
    visible,
    isTitle,
    modalForm,
    modalFormRefs,
    title,
    open,
    close,
    submit
  }
}
```

#### 4.2 ts版

```typescript
import { ref, Ref, computed } from 'vue'

interface resultFn<T> {
  visible: Ref<boolean>
  isTitle: Ref<boolean>
  modalForm: T
  modalFormRefs: any
  title: Ref<string>
  open: Function
  close: Function
  submit: Function
}

interface defaultFace<T> {
  defaultForm?: T
  add?: Function
  edit?: Function
}

/**
 * 弹窗操作
 * @param { params } defaultForm 默认参数
 * @param { params } add 
 * @param { params } edit 
 * @return { resultFn } 
*/
export function useModal<paramsForm, resultForm>(params: defaultFace<paramsForm>): resultFn<resultForm> {
  const visible = ref<boolean>(false)
  const isTitle = ref<boolean>(true)
  const modalForm = ref<resultForm>(params.defaultForm || {})
  const modalFormRefs = ref<any>(null)
  const title = computed(() => isTitle.value ? '添加' : '修改')
  
  function open() {
    visible.value = true
  }

  function close() {
    visible.value = false
    isTitle.value = true
    modalForm.value = params.defaultForm || {}
    modalFormRefs.value && modalFormRefs.value.resetFileds && modalFormRefs.value.resetFileds()
  }

  function submit() {
    modalFormRefs.value && modalFormRefs.value.validate(valid => {
      if(!valid) return
      isTitle.value ? params.add(modalForm.value) : params.edit(modalForm.value)
    })
  }

  return {
    visible,
    isTitle,
    modalForm,
    modalFormRefs,
    title,
    open,
    close,
    submit
  }
}
```