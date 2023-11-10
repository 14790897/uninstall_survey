<template>
  <div class="container mx-auto p-8 bg-white rounded-lg shadow-lg">
    <h1 class="text-2xl font-bold text-indigo-600 mb-6">We're sad to see you go!</h1>
    <form @submit.prevent="sendFeedback">
      <div class="mb-6">
        <label for="email" class="block text-sm font-medium text-gray-700 mb-2">Your Email(Optional)</label>
        <input type="email" id="email" v-model="survey.email"
          class="mt-1 block w-full pl-3 pr-10 py-3 bg-gray-50 text-base border border-gray-300 focus:outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-500 rounded-md shadow-sm" />
      </div>
      <div class="mb-6">
        <label for="reason" class="block text-sm font-medium text-gray-700 mb-2">Why did you uninstall the
          extension?</label>
        <div v-for="(option, index) in options" :key="index" class="mb-4 flex items-center ">
          <input type="radio" :id="`option-${index}`" v-model="survey.reason" :value="option.value"
            class="mt-1 mx-7 block transition duration-300 ease-in-out cursor-pointer h-6 w-6 border-gray-300 text-indigo-600 focus:border-indigo-500 focus:ring-indigo-500" />
          <label :for="`option-${index}`" class="block text-sm font-medium text-gray-700 mb-1">{{ option.text }}</label>
        </div>
      </div>
      <div v-if="survey.reason !== ''" class="mb-6">
        <label for="feedback" class="block text-sm font-medium text-gray-700 mb-2">Please provide more details(Optional)</label>
        <textarea id="feedback" v-model="survey.feedback" rows="4"
          class="mt-1 block w-full p-3 bg-gray-50 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:border-indigo-500 focus:ring-2 focus:ring-indigo-500"></textarea>
      </div>
      <button type="submit"
        class="px-6 py-3 bg-indigo-600 text-white font-semibold rounded-md hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 shadow-lg transition duration-300 ease-in-out">
        Submit Feedback
      </button>
    </form>
  </div>
</template>


<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';

const survey = ref({
  email: 'example@gmial.com',
  reason: '',
  feedback: ''
});

const options = [
  { value: "It's not what I expected", text: "It's not what I expected" },
  { value: "I didn't use it much", text: "I didn't use it much" },
  {
    value: "I had technical issues", text: "I had technical issues"
  },
  { value: "Other", text: "Other" }
];

const API_URL = 'https://serverless.liuweiqing.top/api/sendEmail'
const sendFeedback = async () => {
  try {
    const res = await axios.post(API_URL, {
      email: survey.value.email,
      feedback: survey.value.reason+survey.value.feedback
    });
    if (res.status >= 200 && res.status < 300) {
      alert('Feedback sent successfully!');
      survey.value.email = '';
      survey.value.reason = '';
      survey.value.feedback = '';
    }
  } catch (error) {
    alert('Failed to send feedback. ' + error);
    console.error('Failed to send feedback:', error);
  }
};
</script>
