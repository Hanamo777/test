<template>
  <div class="test">
    <h1>테스트 페이지</h1>
    <p>CI/CD 테스트를 위한 페이지입니다.</p>
    <button @click="$router.push('/')" class="home-button">홈으로 돌아가기</button>
  </div>
</template>

<script>
export default {
  name: 'TestView'
}
</script>

<style scoped>
.test {
  text-align: center;
  padding: 2rem;
}

.home-button {
  padding: 1rem 2rem;
  font-size: 1.2rem;
  background-color: #2196F3;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.home-button:hover {
  background-color: #1976D2;
}
</style> 