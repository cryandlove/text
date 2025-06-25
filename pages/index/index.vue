<template>
	
	<view id="index-area-top" class="index-content-area-top position-top long-view">
	</view>
	<!-- <view @mousemove="handleMouseMove" class="index-content move-with-mouse">
	    <view 
	      class="moveWithMouse"
	      :style="{ left: `${mousePosition.x}rpx`, top: `${mousePosition.y}rpx`, position: 'fixed' }"
	    ></view>
	</view> -->
	<view @mousemove="handleMouseMove"  class="index-content animate-item"  >
		<view
			v-show="moveShowIcon"
			class="moveWithMouse"
			:style="{ left: `${mousePosition.x - 25}rpx`, top: `${mousePosition.y -25}rpx`, position: 'fixed' }"
		></view>
		<view style='font-size: 50px; align-items: center;justify-self: center;'>
			<button>
				<text style='font-size: 50px;'>测试</text>
			</button>
		</view>
		<view 
			class="item-content-index animate-item"
			:class="'even-number'"
		></view>
		<view 
			class="item-content-index animate-item"
			:class="'odd-number'"
		></view>
		<view 
			class="item-content-index animate-item"
			:class="'even-number'"
		></view>
		<view 
			class="item-content-index animate-item"
			:class="'odd-number'"
		></view>
		<view 
			class="item-content-index animate-item item-move-to-center"
		>
			<view class="view-move-to">
				<view id="myElement" class="view-left-to-right">
					<view class="item-list-one"
						:class="'even-number'" style=""></view>
					<view class="item-list-one"
						:class="'odd-number'"></view>
					<view class="item-list-one"
						:class="'even-number'"></view>
					<view class="item-list-one"
						:class="'odd-number'"></view>
					<view class="item-list-one"
						:class="'even-number'"></view>
					<view class="item-list-one"
						:class="'odd-number'"></view>
					<view class="item-list-one"
						:class="'even-number'"></view>
					<view class="item-list-one"
						:class="'odd-number'"></view>
					<view class="item-list-one"
						:class="'even-number'"></view>
					<view class="item-list-one"
						:class="'odd-number'"></view>
				</view>
				
				<view id="myElement-right" class="view-left-to-right" >
					<view class="item-list-one"
						:class="'even-number'" style=""></view>
					<view class="item-list-one"
						:class="'odd-number'"></view>
					<view class="item-list-one"
						:class="'even-number'"></view>
					<view class="item-list-one"
						:class="'odd-number'"></view>
					<view class="item-list-one"
						:class="'even-number'"></view>
					<view class="item-list-one"
						:class="'odd-number'"></view>
					<view class="item-list-one"
						:class="'even-number'"></view>
					<view class="item-list-one"
						:class="'odd-number'"></view>
					<view class="item-list-one"
						:class="'even-number'"></view>
					<view class="item-list-one"
						:class="'odd-number'"></view>
				</view>
			</view>
			
		</view>
		<view 
			class="item-content-index animate-item"
			:class="'odd-number'"
		></view>
		<view 
			class="item-content-index animate-item"
			:class="'even-number'"
		></view>
		<view 
			class="item-content-index animate-item"
			:class="'odd-number'"
		></view>
	</view>
</template>

<script setup>
import { onMounted, ref, getCurrentInstance ,onUpdated } from 'vue';

const innerWidth = window.innerWidth;

const mousePosition = ref({ x: 0, y: 0 });
const moveShowIcon = ref(false)

function handleMouseMove(event) {
	const { clientX, clientY } = event.touches ? event.touches[0] : event;
	const scrollTop = window.scrollY || document.documentElement.scrollTop;
	if(innerWidth > 900){
		moveShowIcon.value = true;
		mousePosition.value = { x: clientX * 2, y: clientY * 2 + scrollTop * 2 };
	}
}



// function moveWhthMouseMethod(ev) {
//   mousePosition.value = { x: ev.clientX, y: ev.clientY };
// }
//onMounted 钩子函数，用于在组件挂载完成后执行某些操作
onMounted(() => {
	const items = document.querySelectorAll('.animate-item')
	// 创建 IntersectionObserver 实例 , 
	// IntersectionObserver是浏览器原生提供的构造函数，接受两个参数：callback是可见性变化时的回调函数，option是配置对象
	// 开始观察
	// observer.observe(document.getElementById('example'));
	// 停止观察
	// observer.unobserve(element);
	// 关闭观察器
	// observer.disconnect();
	const observer = new IntersectionObserver((entries) => {
		entries.forEach(async entry => {
			if (entry.isIntersecting) {
				entry.target.classList.add('animate-in');
			} else {
				// 当元素离开视口时，移除 animate-in 类
				entry.target.classList.remove('animate-in');
			}
		})
	}, {
		rootMargin: '48px',
		threshold: 0.1
	})
	items.forEach(item => {
		observer.observe(item)
	})
	
	
	
	window.addEventListener('scroll', handleScroll);
	let lastScrollTop = 0; // 存储上一次滚动的位置
	function handleScroll() {
		const innerHeight = window.innerHeight;
		    const elScroll = document.getElementById('index-area-top');
		
		    if (elScroll) {
		        const rect = elScroll.getBoundingClientRect();
		        const topDistance = rect.top;
		
		        // 获取当前滚动位置
		        const scrollTop = window.scrollY || document.documentElement.scrollTop;
		
		        // 判断滚动方向：true 表示向上滚动，false 表示向下滚动
		        const isScrollingUp = scrollTop < lastScrollTop;
		        lastScrollTop = scrollTop;
		
		        // 判断元素是否在可视区域内
		        if (topDistance >= 0 && topDistance <= innerHeight) {
		            if (isScrollingUp) {
		                // 向上滑动时添加类
		                elScroll.classList.add('long-view');
		            } else {
		                // 向下滑动时移除类
		                elScroll.classList.remove('long-view');
		            }
		        }
		    }
		
		
		
		// 处理 myElement-left
		const elLeft = document.getElementById('myElement');
		if (elLeft) {
			const rect = elLeft.getBoundingClientRect();
			const topDistance = rect.top;
			if (topDistance >= 0 && topDistance <= innerHeight) {
				let moveP = (innerHeight - topDistance) / innerHeight;
				elLeft.style.transform = `translate(${-innerWidth/2 + innerWidth * moveP}px)`;
			}
		}
	
		// 处理 myElement-right
		const elRight = document.getElementById('myElement-right');
		if (elRight) {
			const rect = elRight.getBoundingClientRect();
			const topDistance = rect.top;
			if (topDistance >= 0 && topDistance <= innerHeight) {
				let moveP = (innerHeight - topDistance) / innerHeight;
				elRight.style.transform = `translate(${innerWidth - innerWidth/2 - innerWidth * moveP}px)`;
			}
		}
		
	}
	
	
	// window.addEventListener('mousemove', moveWhthMouseMethod);
})
</script>

<style scoped lang="scss">
.moveWithMouse {
	width: 50rpx;
	height: 50rpx;
	background-color: #000;
	opacity: 0.6;
	border-radius: 25rpx;
	z-index: 9999 !important; /* 提高优先级 */
	pointer-events: none; /* 确保可以响应事件 */
}

.index-content {
	justify-content: center;
	align-content: center;
	padding: 48rpx;
}
.index-content-area-top{
	margin-bottom: -112rpx;
}
.position-top{
	position: sticky;
	align-self: start;
	top: 40px;
	left: 0px;
	background-color: #000;
	// width: 10%;
	width: 200rpx;
	height: 112rpx;
	z-index: 999;
	transition: width 0.8s ease-out;
}
.position-top.long-view{
	background-color: #000;
	// width: 20%;
	// height: 200rpx;
	width: 112rpx;
	height: 112rpx;
	z-index: 999;
	transition: width 0.8s ease-out;
}
.item-content-index {
	width: 100%;
	height: 400rpx;
	border-radius: 16rpx;
	justify-content: center;
	align-items: center;
	// margin: 48rpx;
	margin: 48rpx  0rpx 48rpx  0rpx;
	pointer-events: none;
}

.even-number {
	background-color: #d9a52c;
}

.odd-number {
	background-color: #4fc8c4;
}
// 知识点
// 静态item
.animate-item {
	opacity: 0;
	transform: translateY(40px);
	filter: blur(2px);
	transition: opacity 0.8s ease-out, transform 0.8s ease-out, filter 0.8s ease-out;
}
// 动画item opacity 01,y  -40 ----> 0,  blur 2px--->0px
.animate-item.animate-in {
	opacity: 1;
	transform: translateY(0);
	filter: blur(0);
}
.view-move-to{
	flex-direction: column;
	justify-content: space-between;
}
.item-move-to-center{
	height: 100%;
	flex-direction: column;
	justify-content: center;
}
.view-left-to-right{
	display: flex;
	flex-direction: row;
	justify-content: space-around;
	margin: 24rpx 0rpx 24rpx 0rpx;
	width: auto;
	border: sandybrown 1px solid;
	opacity: 0.8;
	height: 100%;
}
.item-list-one{
	width: 100rpx;
	height: 100rpx;
	align-self: center;
	margin: 24rpx 12rpx 24rpx 12rpx;
}
</style>