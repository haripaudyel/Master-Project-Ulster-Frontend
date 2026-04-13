<template>
   <admin-layout>
      <PageBreadcrumb :pageTitle="'Chats'" />
      <div>
         <div class="h-[calc(100vh-186px)] overflow-hidden sm:h-[calc(100vh-174px)]">
            <div class="flex h-full flex-col overflow-hidden rounded-2xl border border-gray-200 bg-white dark:border-gray-800 dark:bg-white/[0.03] xl:w-4/4">
               <!-- ====== Chat Box Start -->

               <!-- <div class="custom-scrollbar max-h-full flex-1 space-y-6 overflow-auto p-5 xl:space-y-8 xl:p-6">
                  <div class="max-w-[350px]">
                     <div class="flex items-start gap-4">
                        <div class="h-10 w-full max-w-10 rounded-full">
                           <img src="" alt="profile" class="h-full w-full overflow-hidden rounded-full object-cover object-center">
                        </div>

                        <div>
                           <div class="rounded-lg rounded-tl-sm bg-gray-100 px-3 py-2 dark:bg-white/5">
                              <p class="text-sm text-gray-800 dark:text-white/90">
                                 I want to make an appointment tomorrow from 2:00 to 5:00pm?
                              </p>
                           </div>
                           <p class="mt-2 text-theme-xs text-gray-500 dark:text-gray-400">
                              Lindsey, 2 hours ago
                           </p>
                        </div>
                     </div>
                  </div>

                  <div class="ml-auto max-w-[350px] text-right">
                     <div class="ml-auto max-w-max rounded-lg rounded-tr-sm bg-brand-500 px-3 py-2 dark:bg-brand-500">
                        <p class="text-sm text-white dark:text-white/90">
                           If don’t like something, I’ll stay away from it.
                        </p>
                     </div>
                     <p class="mt-2 text-theme-xs text-gray-500 dark:text-gray-400">
                        2 hours ago
                     </p>
                  </div>

                  <div class="max-w-[350px]">
                     <div class="flex items-start gap-4">
                        <div class="h-10 w-full max-w-10 rounded-full">
                           <img src="" alt="profile" class="h-full w-full overflow-hidden rounded-full object-cover object-center">
                        </div>

                        <div>
                           <div class="rounded-lg rounded-tl-sm bg-gray-100 px-3 py-2 dark:bg-white/5">
                              <p class="text-sm text-gray-800 dark:text-white/90">
                                 I want more detailed information.
                              </p>
                           </div>

                           <p class="mt-2 text-theme-xs text-gray-500 dark:text-gray-400">
                              Lindsey, 2 hours ago
                           </p>
                        </div>
                     </div>
                  </div>

                  <div class="ml-auto max-w-[350px] text-right">
                     <div class="ml-auto max-w-max rounded-lg rounded-tr-sm bg-brand-500 px-3 py-2 dark:bg-brand-500 dark:text-white/90">
                        <p class="text-sm text-white dark:text-white/90">
                           If don’t like something, I’ll stay away from it.
                        </p>
                     </div>

                     <div class="ml-auto mt-2 max-w-max rounded-lg rounded-tr-sm bg-brand-500 px-3 py-2 dark:bg-brand-500">
                        <p class="text-sm text-white dark:text-white/90">
                           They got there early, and got really good seats.
                        </p>
                     </div>

                     <p class="mt-2 text-theme-xs text-gray-500 dark:text-gray-400">
                        2 hours ago
                     </p>
                  </div>

                  <div class="max-w-[350px]">
                     <div class="flex items-start gap-4">
                        <div class="h-10 w-full max-w-10 rounded-full">
                           <img src="" alt="profile" class="h-full w-full overflow-hidden rounded-full object-cover object-center">
                        </div>

                        <div>
                           <div class="mb-2 w-full max-w-[270px] overflow-hidden rounded-lg">
                              <img src="" alt="chat">
                           </div>
                           <div class="max-w-max rounded-lg rounded-tl-sm bg-gray-100 px-3 py-2 dark:bg-white/5">
                              <p class="text-sm text-gray-800 dark:text-white/90">
                                 Please preview the image
                              </p>
                           </div>

                           <p class="mt-2 text-theme-xs text-gray-500 dark:text-gray-400">
                              Lindsey, 2 hours ago
                           </p>
                        </div>
                     </div>
                  </div>
               </div> -->
               
               <div class="custom-scrollbar max-h-full flex-1 space-y-6 overflow-auto p-5">
   
                <div v-for="(msg, index) in messages" :key="index">
                    
                    <!-- USER MESSAGE -->
                    <div v-if="msg.type === 'user'" class="ml-auto max-w-[350px] text-right">
                      <div class="ml-auto max-w-max rounded-lg bg-brand-500 px-3 py-2">
                          <p class="text-sm text-white">
                            {{ msg.text }}
                          </p>
                      </div>
                    </div>

                    <!-- BOT MESSAGE -->
                    <div v-else class="max-w-[350px]">
                      <div class="rounded-lg bg-gray-100 px-3 py-2">
                          <p class="text-sm text-gray-800">
                            {{ msg.text }}
                          </p>
                      </div>
                    </div>

                </div>

                <!-- Loading -->
                <div v-if="loading" class="text-sm text-gray-500">
                    Typing...
                </div>

               </div>
               <div class="sticky bottom-0 border-t border-gray-200 p-3 dark:border-gray-800">
                  <form @submit.prevent="sendMessage" class="flex items-center justify-between">
                     <div class="relative w-full">
                        

                        <input v-model="userInput" type="text" placeholder="Ask anything about ulster University..." class="h-9 w-full border-none bg-transparent pl-12 pr-5 text-sm text-gray-800 outline-hidden placeholder:text-gray-400 focus:border-0 focus:ring-0 dark:text-white/90">
                     </div>

                     <div class="flex items-center">
                        

                        <button type="submit" class="ml-3 flex h-9 w-9 items-center justify-center rounded-lg bg-brand-500 text-white hover:bg-brand-600 xl:ml-5">
                           <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                              <path fill-rule="evenodd" clip-rule="evenodd" d="M4.98481 2.44399C3.11333 1.57147 1.15325 3.46979 1.96543 5.36824L3.82086 9.70527C3.90146 9.89367 3.90146 10.1069 3.82086 10.2953L1.96543 14.6323C1.15326 16.5307 3.11332 18.4291 4.98481 17.5565L16.8184 12.0395C18.5508 11.2319 18.5508 8.76865 16.8184 7.961L4.98481 2.44399ZM3.34453 4.77824C3.0738 4.14543 3.72716 3.51266 4.35099 3.80349L16.1846 9.32051C16.762 9.58973 16.762 10.4108 16.1846 10.68L4.35098 16.197C3.72716 16.4879 3.0738 15.8551 3.34453 15.2223L5.19996 10.8853C5.21944 10.8397 5.23735 10.7937 5.2537 10.7473L9.11784 10.7473C9.53206 10.7473 9.86784 10.4115 9.86784 9.99726C9.86784 9.58304 9.53206 9.24726 9.11784 9.24726L5.25157 9.24726C5.2358 9.20287 5.2186 9.15885 5.19996 9.11528L3.34453 4.77824Z" fill="white"></path>
                           </svg>
                        </button>
                     </div>
                  </form>
               </div>
               <!-- ====== Chat Box End -->
            </div>
         </div>
      </div>
   </admin-layout>
</template>

<script>
import { ref } from 'vue'
import axios from 'axios'

import AdminLayout from '../components/layout/AdminLayout.vue'
import EcommerceMetrics from '../components/ecommerce/EcommerceMetrics.vue'
import MonthlyTarget from '../components/ecommerce/MonthlySale.vue'
import MonthlySale from '../components/ecommerce/MonthlyTarget.vue'
import CustomerDemographic from '../components/ecommerce/CustomerDemographic.vue'
import StatisticsChart from '../components/ecommerce/StatisticsChart.vue'
import RecentOrders from '../components/ecommerce/RecentOrders.vue'
import PageBreadcrumb from '../components/common/PageBreadcrumb.vue'

export default {
   name: 'Ecommerce',

   components: {
      AdminLayout,
      EcommerceMetrics,
      MonthlyTarget,
      MonthlySale,
      CustomerDemographic,
      StatisticsChart,
      RecentOrders,
      PageBreadcrumb,
   },

   setup() {
      // state
      const messages = ref([
         {
            type: 'bot',
            text: 'Ask anything about Ulster University...'
         }
      ])

      const userInput = ref('')
      const loading = ref(false)

      // function
      const sendMessage = async () => {
         if (!userInput.value.trim()) return

         // push user message
         messages.value.push({
            type: 'user',
            text: userInput.value
         })

         const question = userInput.value
         userInput.value = ''
         loading.value = true

         try {
            const res = await axios.post('http://127.0.0.1:8000/chat', {
               question: question
            })

            messages.value.push({
               type: 'bot',
               text: res.data.reply
            })
         } catch (error) {
            messages.value.push({
               type: 'bot',
               text: 'Something went wrong. Please try again.'
            })
         } finally {
            loading.value = false
         }
      }

      // expose to template
      return {
         messages,
         userInput,
         loading,
         sendMessage
      }
   }
}
</script>
