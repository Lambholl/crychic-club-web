
<script setup lang="ts">
import RotateImage from '../components/RotateImage.vue';
import { ElSpace, ElContainer, ElMain, ElButton, ElRow, ElCol } from 'element-plus';

const button = {
  type: 'warning',
  color: '#fcd34d',
  round: true,
}
</script>

<template>
  <el-container>
    <el-main class="home-container">
        <el-row justify="center">
          <el-col :xs="24" :sm="20" :md="18" :lg="16">
            <RotateImage src="/imgs/home/main.webp" alt="乐队养的耄耋" :max-rotate="3" />
          </el-col>
        </el-row>
        <el-row justify="center">
          <h1 class="title">欢迎来到 Crychic 乐队</h1>
        </el-row>
        <el-row justify="center">
          <el-button class="explore-button" href="https://github.com/Lambholl/crychic-club-web" target="_blank" :round="button.round" :color="button.color" tag="a">咕咕嘎嘎</el-button>
        </el-row>
    </el-main>
  </el-container>
</template>


<style>

.home-container {
  background: linear-gradient(135deg, #ff9a9e, #fad0c4);
  min-height: 100vh;
  padding: 20px;
  display: block;
}

.title {
  font-size: 2.5rem;
  color: #333;
  margin: 20px 0 10px;
  text-align: center;
}

.description {
  font-size: 1.2rem;
  color: #555;
  margin-bottom: 20px;
}

.explore-button {
  cursor: pointer;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
