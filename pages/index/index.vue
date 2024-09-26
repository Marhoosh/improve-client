<template>
  <div class="container">
    <h1>{{ isEditing ? "更新计划" : "创建计划" }}</h1>
    <form @submit.prevent="submitPlan">
      <div class="form-group">
        <label for="name">计划名称</label>
        <input v-model="plan.name" id="name" type="text" placeholder="输入计划名称" required />
      </div>

      <div class="form-group">
        <label for="details">计划详情</label>
        <textarea v-model="plan.details" id="details" placeholder="输入计划详情" required></textarea>
      </div>

      <div class="form-group">
        <label for="progress">实际完成情况</label>
        <input v-model="plan.progress" id="progress" type="text" placeholder="输入完成情况" />
      </div>

      <div class="form-group">
        <label for="date">日期</label>
        <input v-model="plan.date" id="date" type="date" required />
      </div>

      <div class="form-group">
        <label for="estimatedTime">预计耗时 (小时)</label>
        <input v-model.number="plan.estimatedTime" id="estimatedTime" type="number" placeholder="输入预计耗时" required />
      </div>

      <div class="form-group">
        <label for="actualTime">实际耗时 (小时)</label>
        <input v-model.number="plan.actualTime" id="actualTime" type="number" placeholder="输入实际耗时" />
      </div>

      <div class="form-group">
        <label for="completed">是否完成</label>
        <select v-model="plan.completed" id="completed">
          <option :value="false">未完成</option>
          <option :value="true">已完成</option>
        </select>
      </div>

      <div class="form-group">
        <label for="remarks">备注</label>
        <textarea v-model="plan.remarks" id="remarks" placeholder="输入备注"></textarea>
      </div>

      <button type="submit">{{ isEditing ? "更新计划" : "创建计划" }}</button>
    </form>

    <!-- 显示计划列表 -->
    <div v-if="plans.length > 0">
      <h2>计划列表</h2>
      <ul>
        <li v-for="(p, index) in plans" :key="index">
          <strong>{{ p.name }}</strong> - {{ p.details }} ({{ p.date }})
          <button @click="editPlan(index)">编辑</button>
          <button @click="deletePlan(index)">删除</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue'

// 计划的初始值
const initialPlan = {
  name: '',
  details: '',
  progress: '',
  date: '',
  estimatedTime: 0,
  actualTime: 0,
  completed: false,
  remarks: ''
}

// 当前的计划数据
const plan = reactive({ ...initialPlan })
const plans = ref([])
const isEditing = ref(false)
let editingIndex = null

// 提交计划
const submitPlan = () => {
  if (isEditing.value) {
    // 更新计划
    plans.value[editingIndex] = { ...plan }
    isEditing.value = false
  } else {
    // 创建新计划
    plans.value.push({ ...plan })
  }
  resetForm()
}

// 编辑计划
const editPlan = (index) => {
  editingIndex = index
  Object.assign(plan, plans.value[index])
  isEditing.value = true
}

// 删除计划
const deletePlan = (index) => {
  plans.value.splice(index, 1)
}

// 重置表单
const resetForm = () => {
  Object.assign(plan, { ...initialPlan })
}
</script>

<style lang="scss">
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

h1, h2 {
  text-align: center;
}

.form-group {
  margin-bottom: 15px;

  label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
  }

  input,
  textarea,
  select {
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  textarea {
    resize: vertical;
  }
}

button {
  display: block;
  width: 100%;
  padding: 10px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

button:hover {
  background-color: #218838;
}

ul {
  list-style: none;
  padding: 0;

  li {
    margin-bottom: 10px;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
    display: flex;
    justify-content: space-between;
    align-items: center;

    button {
      margin-left: 10px;
      background-color: #007bff;
      font-size: 14px;
    }

    button:hover {
      background-color: #0056b3;
    }
  }
}
</style>
