<template>
	<view class="container">
		<view class="form-group">
			<text>计划名称:</text>
			<input v-model="plan.name" placeholder="请输入计划名称" />
		</view>

		<view class="form-group">
			<text>计划详情:</text>
			<textarea v-model="plan.details" placeholder="请输入计划详情"></textarea>
		</view>

		<view class="form-group">
			<text>预计耗时(小时):</text>
			<input v-model="plan.estimatedTime" placeholder="请输入预计耗时" type="number" />
		</view>

		<view class="form-group">
			<text>计划日期:</text>
			<picker mode="date" v-model="plan.date">
				<view>{{ plan.date || '请选择日期' }}</view>
			</picker>
		</view>

		<button @click="createPlan">创建计划</button>
	</view>
</template>

<script setup>
	import {
		reactive
	} from 'vue'
	// import {
	// 	showToast
	// } from '@dcloudio/uni-app'

	const plan = reactive({
		name: '',
		details: '',
		estimatedTime: '',
		date: ''
	})

	const createPlan = () => {
		if (!plan.name || !plan.details || !plan.estimatedTime || !plan.date) {
			uni.showToast({
				title: '请填写完整信息',
				icon: 'none'
			})
			return
		}

		// 模拟保存逻辑
		console.log('计划已创建:', plan)
		// uni.showToast({
			
		// })
		uni.showToast({
			title: '计划创建成功',
			icon: 'success'
		})

		// 重置表单
		plan.name = ''
		plan.details = ''
		plan.estimatedTime = ''
		plan.date = ''
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