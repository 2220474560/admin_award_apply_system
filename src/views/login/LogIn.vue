<!--
    * @FileDescription: 登录页面。
    * @Author: 作者信息
    * @Date: 2024年1月22日
    * @LastEditors: 李思佳
    * @LastEditTime: 2024年1月22日
-->
<template>
  <div>
    <h2>登录</h2>
    <a-button type="primary" ghost @click="logIn">登录</a-button>
    <a-button type="primary" ghost @click="learningProgress">学习之星与进步之星</a-button>
    <a-button type="primary" ghost @click="matchStar">竞赛之星</a-button>
    <a-button type="primary" ghost @click="researchStar">科研之星</a-button>
    <a-button type="primary" ghost @click="doubleStar">双创之星</a-button>
  </div>
</template>

<script setup lang="ts">
import router from '@/routers'

function logIn() {
  router.push('/DoubleStar')
}

function doubleStar() {
  router.push('/DoubleStar')
}
function learningProgress() {
  router.push('/LearningProgress')
}
function matchStar() {
  router.push('/MatchStar')
}
function researchStar() {
  router.push('/ResearchStar')
}
</script>

<style scoped></style>
