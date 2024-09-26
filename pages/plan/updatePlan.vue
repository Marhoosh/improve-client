<template>
	<view class="container">
		<view class="form-group">
			<text>计划名称:</text>
			<input v-model="plan.name" placeholder="请输入计划名称" />
		</view>

		<view class="form-group">
			<text>实际完成情况:</text>
			<textarea v-model="plan.actualCompletion" placeholder="请输入实际完成情况"></textarea>
		</view>

		<view class="form-group">
			<text>实际耗时(小时):</text>
			<input v-model="plan.actualTime" placeholder="请输入实际耗时" type="number" />
		</view>

		<view class="form-group">
			<text>是否完成:</text>
			<switch v-model="plan.isCompleted" />
		</view>

		<view class="form-group">
			<text>备注:</text>
			<textarea v-model="plan.notes" placeholder="请输入备注"></textarea>
		</view>

		<button @click="updatePlan">更新计划</button>
	</view>
</template>

<script setup>
	import {
		reactive
	} from 'vue'
	// import { showToast } from '@dcloudio/uni-app'

	const plan = reactive({
		name: '默认计划名称', // 假设这里是从数据库读取出来的计划
		actualCompletion: '',
		actualTime: '',
		isCompleted: false,
		notes: ''
	})

	const updatePlan = () => {
		if (!plan.name || !plan.actualCompletion || !plan.actualTime) {
			uni.showToast({
				title: '请填写完整信息',
				icon: 'none'
			})
			return
		}

		// 模拟更新逻辑
		console.log('计划已更新:', plan)
		uni.showToast({
			title: '计划更新成功',
			icon: 'success'
		})
	}
</script>

<style lang="scss" scoped>
	.container {
		padding: 20px;
	}

	.form-group {
		margin-bottom: 20px;
	}

	input,
	textarea {
		width: 100%;
		padding: 10px;
		border: 1px solid #ddd;
		border-radius: 5px;
	}

	button {
		background-color: #007aff;
		color: white;
		padding: 10px;
		border-radius: 5px;
		text-align: center;
	}
</style>