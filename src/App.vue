<template>
	<div class="menu">
		<a href="javascript:;" v-for="(ele, idx) in items" :key="idx">{{ ele }}</a>
	</div>
	<div v-for="(ele, idx) in data" :key="ele.id">
		<div class="img">
			<img :src="ele.image" alt="" />
		</div>
		<h4 class="red" :style="colorBlue" @click="openpop">{{ ele.title }}</h4>
		<p>{{ ele.content }}</p>
		<p>{{ ele.price }} 만원</p>
		<button @click="increase(idx)">허위매물신고</button>
		<span>신고수 : {{ count[idx] }}</span>
	</div>

	<!-- modal area -->
	<div class="black-bg" v-if="modal == true">
		<div class="white-bg">
			<h4>모달 제목</h4>
			<p>모달 내용</p>
			<button @click="closepop">닫기</button>
		</div>
	</div>
</template>

<script>
import productData from '@/assets/data.js';

export default {
	name: 'App',
	data() {
		return {
			data: productData,
			modal: false,
			count: [0, 0, 0],
			price: [60, 70, 80],
			colorBlue: 'color: blue',
			products: [
				{
					imgSrc: require('@/assets/images/room0.jpg'), //일반 경로는 string 이므로 require 사용하여 변환
					imgAlt: '이미지1',
					address: '역삼동',
				},
				{
					imgSrc: require('@/assets/images/room1.jpg'),
					imgAlt: '이미지2',
					address: '천호동',
				},
				{
					imgSrc: require('@/assets/images/room2.jpg'),
					imgAlt: '이미지3',
					address: '마포구',
				},
			],
			items: ['HOME', 'PRODUCTS', 'ABOUT'],
		};
	},
	methods: {
		increase(idx) {
			this.count[idx] += 1;
		},
		imgsrc() {
			console.log(
				document.body.querySelector('.img img').getAttribute('src').split('/'),
			);
		},
		openpop() {
			console.log(this.modal);
			if (this.modal == false) {
				this.modal = true;
			}
		},
		closepop() {
			if (this.modal == true) {
				this.modal = false;
			}
		},
	},
	components: {},
};
</script>

<style>
body {
	margin: 0;
	padding: 0;
}
div {
	box-sizing: border-box;
}
.img {
	width: 100%;
	margin-top: 40px;
}
.img img {
	width: 100%;
}
.red {
	color: red;
}
.menu {
	display: flex;
	width: 100%;
	background: darkslateblue;
	border-radius: 5px;
}
.menu a {
	display: block;
	flex: 1;
	padding: 15px;
	color: white;
	font-size: 16px;
	text-align: center;
}
.black-bg {
	width: 100%;
	height: 100%;
	background: rgba(0, 0, 0, 0.5);
	position: fixed;
	top: 0;
	padding: 15px;
}
.white-bg {
	width: 100%;
	background: white;
	border-radius: 10px;
	padding: 15px;
}
</style>
