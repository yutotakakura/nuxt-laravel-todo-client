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
                <th scope="col" class="px-6 py-3">
                    詳細
                </th>
                <th scope="col" class="px-6 py-3">
                    編集
                </th>
                <th scope="col" class="px-6 py-3">
                    削除
                </th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="task in tasks" :key="task.id" class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                    {{ task.title }}
                </th>
                <td class="px-6 py-4">
                    {{ task.content }}
                </td>
                <td class="px-6 py-4">
                    {{ task.person_in_charge }}
                </td>
                <td class="px-6 py-4">
                  <NuxtLink
                    :to="`/${task.id}`"
                    class="shadow bg-slate-500 hover:bg-slate-400 focus:shadow-outline focus:outline-none text-white font-bold py-2 px-4 rounded"
                    type="button">詳細</NuxtLink>
                </td>
                <td class="px-6 py-4">
                  <NuxtLink
                    :to="`/edit/${task.id}`"
                    class="shadow bg-slate-500 hover:bg-slate-400 focus:shadow-outline focus:outline-none text-white font-bold py-2 px-4 rounded"
                    type="button">編集</NuxtLink>
                </td>
                <td class="px-6 py-4">
                  <NuxtLink 
                    to="/" 
                    class="shadow bg-slate-500 hover:bg-slate-400 focus:shadow-outline focus:outline-none text-white font-bold py-2 px-4 rounded"
                    type="button" @click="deleteTask(task.id)">削除</NuxtLink>
                </td>
            </tr>
        </tbody>
    </table>
  </div>
</template>

<script setup>
  const { data: tasks, refresh } = await useFetch('http://localhost:80/api/tasks')

  const deleteTask = (id) => {
    useFetch('http://localhost:80/api/tasks/' + id, {
      method: 'DELETE',
    }).then(res => refresh())
  };
</script>