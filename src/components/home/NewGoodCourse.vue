<template>
	<div class='new-course'>
		<div class='contentTitle'>
			<div class='contentTitle-left'>
				<div class='hot'>
					<div class='hot-l'>HOT</div>
					<div class='hot-r'></div>
				</div>
				<div class='txt'>
					<div class='txt-top'>新上好课</div>
					<div class='txt-bottom'></div>
				</div>
			</div>
			<div class='more'>更 多</div>
		</div>
		<div class='newCourseContent'>
			<ul>
				<li 
					class='courseItem'
					v-for='item in newCourse'
					:key='item.id'
                    @click="toDetailPage()"
				>
					<div class='courseInfo'>
						<div class='courseBg'>
							<img :src="item.cover">
						</div>
						<div class="courseName">{{item.name}}</div>
                        <div class="courseDegree">{{ courseTypeFn(item.level) }}  · 100 人报名</div>
                    

						<div class="coursePriceZero" v-if="item.price == 0">
                            <div class="pricefree">免费学习</div>
                            <img src="@/assets/img/free.png" alt="">
                        </div>

                        <div class="coursePrice" v-else-if="item.isMember == 1">
                            <div class="courseMemberbg"><span class="courseMember">会员免费</span></div>
                            <div class="price">¥ {{item.price}}</div>
                        </div>
                        
                        <div class="coursePricePri" v-else>
                            <div class="pricePri">¥ {{item.price}}</div>
                        </div>
					</div>
				</li>
			</ul>
		</div>
	</div>
</template>

<script setup>
import { mostNewCourse } from '@/utils/api/api.js'

import {courseType} from '@/utils/mixins/courseType.js'
let { courseTypeFn } = courseType();
let router = useRouter()
//新上好课的数据
let newCourse = ref([]);

onBeforeMount(()=>{
	mostNewCourse({
		pageNum:1,
		pageSize:8
	}).then(res=>{
		newCourse.value = res.list;
		console.log( res.list )
	})
})
const toDetailPage = () => {
  router.push({
    name: 'courseDetail'
    })
}
</script>

<style scoped>
.new-course{
   	width: 1200px;
    margin: 0 auto;
    margin-top: 15px;
}
.contentTitle{
	display: flex;
	justify-content: space-between;
}
.contentTitle-left{
	display: flex;
}
.hot{
	display: flex;
    height: 38px;
}
.hot-l{
	height: 38px;
    font-size: 20px;
    padding: 0 10px;
    text-align: center;
    line-height: 37px;
    color: #ffffff;
    border-radius: 8px 0 8px 8px;
    background: linear-gradient(90deg, #ff727f 0%, #fc685c 100%);
}
.hot-r{
	width: 0;
    height: 0;
    border: 6px solid #fc685c;
    border-right-color: transparent;
    border-bottom-color: transparent;
}
.txt{
	position: relative;
    height: 38px;
    margin-left: 10px;
}
.txt-top{
	font-size: 24px;
    padding: 0 5px;
    color: #222222;
    line-height: 31px;
}
.txt-bottom{
	position: absolute;
    top: 25px;
    left: 0px;
    width: 100%;
    height: 13px;
    background: linear-gradient(90deg, #fbf84f 0%, #fea935 100%);
    border-radius: 7px;
    z-index: -1;
}
.more{
	cursor: pointer;
    font-size: 14px;
    font-weight: 400;
    color: #337dff;
}
.newCourseContent{
	width: 1200px;
    margin: 30px auto 0px auto;
}
.newCourseContent ul{
	display: flex;
	flex-wrap: wrap;
    padding: 0;
}
.courseItem{
	width: 285px;
    height: 280px;
    margin: 0 20px 20px 0;
    transition: margin-top 0.2s;
    list-style: none;
}
.courseItem:hover{
    margin-top: -10px;
    cursor: pointer;
}
.courseItem:nth-child(4n+0){
    margin-right: 0 !important;
}
.courseInfo{
	position: relative;
    width: 100%;
    height: 270px;
    background: #ffffff;
    box-shadow: 1px 1px 10px rgb(27 39 94 / 40%);
    opacity: 1;
    border-bottom-left-radius: 6px;
    border-bottom-right-radius: 6px;
    overflow: hidden;
    text-decoration: none;
}
.courseBg{
	position: relative;
    width: 100%;
    height: 160px;
}
li{
    list-style-type: none;
}
.courseBg img{
	width: 100%;
    height: 100%;
}
.courseName{
    margin: 10px;
    font-weight: bold;
    font-size: 14px;
    color: #333333;
    display: -webkit-box;
    overflow: hidden;
}
.courseDegree{
    margin-left: 10px;
    font-size: 12px;
    color: #808080;
}
.coursePrice {
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 130px;
    font-size: 14px;
    margin-top: 15px;
    padding: 0 5px;
}
.coursePricePri{
    width: 75px;
    font-size: 14px;
    margin-top: 18px;
    padding: 0 13px;
    color: rgba(255, 114, 127, 1);
    font-weight: 700;
}
.coursePriceZero{
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 75px;
    font-size: 14px;
    margin-top: 15px;
    padding: 0 10px;
    color: rgba(53, 134, 255, 1);
}
.courseMemberbg {
    position: relative;
    width: 80px;
    height: 20px;
    color: #ffffff;
    background: linear-gradient(90deg, #ff928e 0%, #fe7062 99%);
    border-radius: 24px 0px 24px 0px;
}
.courseMember {
    position: absolute;
    line-height: 20px;
    left: 13px;
    font-weight: 700;
}
.price {
    line-height: 25px;
    left: 100px;
    color: #ff727f;
    font-weight: 700;
}
</style>