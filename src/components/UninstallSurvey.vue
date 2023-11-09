<template>
  <div class="container mx-auto p-4">
    <h1 class="text-xl font-bold mb-4">We're sad to see you go!</h1>
    <form @submit.prevent="submitSurvey">
      <div class="mb-4">
        <label for="reason" class="block text-sm font-medium text-gray-700">Why did you uninstall the extension?</label>
        <select id="reason" v-model="survey.reason"
          class="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md">
          <option disabled value="">Please select one</option>
          <option>It's not what I expected</option>
          <option>I didn't use it much</option>
          <option>I had technical issues</option>
          <option>Other</option>
        </select>
      </div>
      <div v-if="survey.reason === 'Other'" class="mb-4">
        <label for="feedback" class="block text-sm font-medium text-gray-700">Please provide more details</label>
        <textarea id="feedback" v-model="survey.feedback" rows="4"
          class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500"></textarea>
      </div>
      <button type="submit" class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-700">Submit Feedback</button>
    </form>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const survey = ref({
  reason: '',
  feedback: ''
});

function submitSurvey() {
  // 在这里处理表单提交，例如发送到服务器
  console.log(survey.value);
  // 通常你会在这里发送一个请求到后端API
  // 但是请确保处理用户的隐私信息
}

</script>

<style scoped>
/* 在这里添加你的TailwindCSS样式，如果需要的话 */
</style>
