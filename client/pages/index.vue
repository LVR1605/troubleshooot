<script setup>
import { assertExpressionStatement } from '@babel/types';
import { ref, onMounted } from "vue";
import axios from "axios";

const currentPage = ref(1);
const perPage = 10;
const totalPages = ref(0);
const user = ref([]);
const pending = ref(false);

onMounted(() => {
  fetchData();
});

async function previousPage() {
  if (currentPage.value > 1) {
    currentPage.value--;
    await fetchData();
  }
}

async function nextPage() {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
    await fetchData();
  }
}

async function fetchData() {
  pending.value = true;

  try {
    const response = await axios.get(`http://127.0.0.1:8000/api/users?page=${currentPage.value}&perPage=${perPage}`);
    user.value = response.data.data;
    totalPages.value = Math.ceil(response.data.total / perPage);
  } catch (error) {
    console.error("Error fetching data:", error);
  } finally {
    pending.value = false;
  }
}

function viewUser(userId) {
  navigateTo('/users/' + userId);
}

function editUser(userId) {
  navigateTo('/users/edit?user_id=' + userId);
}
</script>

<template>
	<div class="mx-auto max-w-5xl py-10">
		<h3 class="text-2xl">Users</h3>
		<div>
		  <FormButton type="button" class="transition-colors duration-200 bg-blue-400 text-black font-semibold text-sm hover:bg-teal-200 p-3 rounded-lg" @click="navigateTo('/users/new')">New User</FormButton>
		</div>
		<div>
		  <div v-if="pending">
			Loading ...
		  </div>
		  <div v-else>
			<table class="min-w-full text-left text-sm font-light">
			  <thead class="border-b font-medium dark:border-neutral-500">
				<tr>
				  <th scope="col" class="px-6 py-2">Name</th>
				  <th scope="col" class="px-6 py-2">Course</th>
				  <th scope="col" class="px-6 py-2">Is Active</th>
				  <th scope="col" class="px-6 py-2">Action</th>
				</tr>
			  </thead>
			  <tbody v-if="user.length > 0">
				<tr class="border-b dark:border-neutral-500" v-for="user in user">
				  <td class="whitespace-nowrap px-6 py-2 font-medium">{{ user.name }}</td>
				  <td class="whitespace-nowrap px-6 py-2">{{ user.course }}</td>
				  <td class="whitespace-nowrap px-6 py-2">
					<span v-if="user.is_active" class="text-green-700">✓</span>
					<span v-else class="text-red-700">X</span>
				  </td>
				  <td class="whitespace-nowrap px-6 py-2">
					<a class="cursor-pointer hover:underline hover:text-gray-700" @click="viewUser(user.id)">
					  View
					</a>
					<a class="cursor-pointer hover:underline hover:text-gray-700" @click="editUser(user.id)">
					  Edit
					</a>
				  </td>
				</tr>
			  </tbody>
			</table>
			</div>
		</div>
		<div class="flex justify-between p-5 m-5 ">
			<FormButtonPage type="button" class="transition-colors duration-200 bg-blue-400 text-black font-semibold text-sm hover:bg-teal-200 p-3 rounded-lg" @click="previousPage" :disabled="currentPage === 1">PREVIOUS</FormButtonPage>
			<FormButtonPage type="button" class="transition-colors duration-200 bg-blue-400 text-black font-semibold text-sm hover:bg-teal-200 p-3 rounded-lg" @click="nextPage" :disabled="currentPage === totalPages">NEXT</FormButtonPage>
			
        </div>
	</div>
</template>
  