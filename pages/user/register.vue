<template>
	<view class="wrap u-p-t-80">
		<!-- u-field为uView表单 -->
		<u-field v-model="name" label="昵称" placeholder="请输入昵称" focus required></u-field>
		<u-field v-model="email" label="邮箱" placeholder="请输入邮箱" required :error-message="emailMsg"></u-field>
		<u-field v-model="password" label="密码" placeholder="请输入密码" required :error-message="pwdMsg" password></u-field>
		<u-field v-model="password_confirmation" label="确认密码" placeholder="请确认密码" required password
			:error-message="errorMessage"></u-field>
		<!-- 动态跟踪样式为inputStyle -->
		<button @tap="submit" :loading="submitBtn" :disabled="submitBtn" :style="[inputStyle]"
			class="getCaptcha">注册</button>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				// 用户注册参数
				name: "",
				email: "",
				password: "",
				password_confirmation: "",
				submitBtn: false,
			};
		},
		computed: {
			inputStyle() {
				let style = {};
				// 全部验证通过，激活注册
				if (this.$u.test.email(this.email) && this.password && this.password == this.password_confirmation &&
					this.name) {
					style.color = "#fff";
					style.backgroundColor = this.$u.color['primary'];
				}
				return style;
			},
			emailMsg() {
				if (!this.email) {
					return ''
				}
				if (!this.$u.test.email(this.email)) {
					return '邮箱格式错误'
				} else {
					return ''
				}
			},
			pwdMsg() {
				if (!this.password) {
					return ''
				}
				if (!this.$u.test.rangeLength(this.password, [6, 12])) {
					return '密码长度需在6-12位'
				} else {
					return ''
				}
			},
			errorMessage() {
				if (this.password !== this.password_confirmation) {
					return '两次密码不一致'
				} else {
					return ''
				}
			}

		}
	}
</script>

<style scoped lang="scss">
	.wrap {
		.getCaptcha {
			width: 90%;
			margin-top: 12rpx;
			background-color: #a2b8ff;
			color: $u-tips-color;
			border: none;
			font-size: 30rpx;
			padding: 12rpx 0;

			&::after {
				border: none;
			}
		}
	}
</style>
