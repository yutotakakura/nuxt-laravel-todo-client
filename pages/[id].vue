<template>
  <div class="relative overflow-x-auto">
    <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
        <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
            <tr>
                <th scope="col" class="px-6 py-3">
                    タイトル
                </th>
                <th scope="col" class="px-6 py-3">
                    内容
                </th>
                <th scope="col" class="px-6 py-3">
                    担当者
                </th>
            </tr>
        </thead>
        <tbody>
            <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                    {{ task.title }}
                </th>
                <td class="px-6 py-4">
                    {{ task.content }}
                </td>
                <td class="px-6 py-4">
                    {{ task.person_in_charge }}
                </td>
            </tr>
        </tbody>
    </table>
    <NuxtLink
      to="/" 
      class="shadow bg-slate-500 hover:bg-slate-400 focus:shadow-outline focus:outline-none text-white font-bold m-6 py-2 px-4 rounded"
      type="button">戻る
  </NuxtLink>
  </div>
</template>

<script setup>
  const route = useRoute()
  const { data: task } = await useFetch('http://localhost:80/api/tasks/' + route.params.id)
</script>