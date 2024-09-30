<template>
	<view class="container">
		<view class="form-group">
			<text>计划名称:</text>
			<input v-model="plan.name" placeholder="请输入计划名称" />
		</view>

		<view class="form-group">
			<text>计划详情:</text>
			<textarea v-model="plan.detail" placeholder="请输入计划详情"></textarea>
		</view>

		<view class="form-group">
			<text>预计耗时(小时):</text>
			<input v-model="plan.expectTime" placeholder="请输入预计耗时" type="number" />
		</view>

		<div class="form-group">
			<label for="date">日期</label>
			<input v-model="plan.date" id="date" type="date" required />
		</div>

		<button @click="createPlan">创建计划</button>
	</view>
</template>

<script setup>
	import {
		reactive
	} from 'vue'

	const plan = reactive({
		name: '',
		detail: '',
		expectTime: '',
		date: ''
	})

	const createPlan = () => {
		if (!plan.name || !plan.detail || !plan.expectTime || !plan.date) {
			uni.showToast({
				title: '请填写完整信息',
				icon: 'none'
			})
			return
		}

		// 发送请求给后端
		uni.request({
			url: 'http://localhost:80/improve/plan/add', // 替换为你的后端接口
			method: 'POST',
			data: plan,
			header: {
				'Content-Type': 'application/json'
			},
			success: (res) => {
				if (res.statusCode === 200) {
					uni.showToast({
						title: '计划创建成功',
						icon: 'success'
					})
					// 重置表单
					resetForm()
				} else {
					uni.showToast({
						title: '创建失败:' + res.data.message,
						icon: 'none'
					})
				}
			},
			fail: (err) => {
				uni.showToast({
					title: '请求失败:' + err.errMsg,
					icon: 'none'
				})
			}
		})
	}

	const resetForm = () => {
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