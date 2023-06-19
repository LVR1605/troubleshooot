<!-- <template>
    <div class="mx-auto max-w-5xl py-10">
        <h3 class="text-2xl">Edit User</h3>
        <div class="py-3">
            <button @click="back()" class="border px-4 py-1 hover:bg-gray-50">Back</button>
        </div>
        <div v-if="pending">
            Loading...
        </div>
        <div v-else>
            <form class="space-y-3" @submit.prevent="updateUser()">
                <div>
                    <FormLabel label="Name" />
                    <FormTextField name="name" placeholder="Name" v-model="state.user.name" />
                    <div>
                        {{ state.errors && state.errors.data && state.errors.data.errors && state.errors.data.errors.name && state.errors.data.errors.name[0] }}
                    </div>
                </div>
                <div>
                    <FormLabel label="Course" />
                    <FormTextField name="course" placeholder="Course" v-model="state.user.course" />
                    <div>
                        {{ state.errors && state.errors.data && state.errors.data.errors && state.errors.data.errors.course && state.errors.data.errors.course[0] }}
                    </div>
                </div>
                <div>
                    <FormLabel label="Email" />
                    <FormTextField name="email" placeholder="email" v-model="state.user.email" />
                    <div>
                        {{ state.errors && state.errors.data && state.errors.data.errors && state.errors.data.errors.email && state.errors.data.errors.email[0] }}
                    </div>
                </div>
                <div>
                    <FormLabel label="Password" />
                    <FormTextField type="password" name="password" placeholder="password" v-model="state.user.password"/>
                    <div>
                        {{ state.errors && state.errors.data && state.errors.data.errors && state.errors.data.errors.password && state.errors.data.errors.password[0] }}
                    </div>
                </div>
                <div>
                    <FormLabel label="Status" />
                    <br />
                    <FormCheckbox :value="state.user.is_active ? true : false"
                        @click="state.user.is_active = !state.user.is_active" />
                </div>
                <div>
                    <FormButton type="submit" buttonStyle="primary" class="w-full">Update</FormButton>
                </div>
            </form>
        </div>
    </div>
</template>
  
<script setup>
const route = useRoute();
const userId = route.query.user_id

const { pending, data: user } = await useLazyAsyncData('user', () => $fetch(`http://127.0.0.1:8000/api/users/${userId}`))

const state = reactive({
    user: {
        name: user && user.value && user.value.name,
        course: user && user.value && user.value.course,
        email: user && user.value && user.value.email,
        password: user && user.value && user.value.password,
        is_active: user && user.value && user.value.is_active,
    }
})

watch(user, (newData) => {
    state.user = {
        name: newData && newData.name,
        course: newData && newData.course,
        email: newData && newData.email,
        password: newData && newData.password,
        is_active: newData && newData.is_active,
    }
})

function back() {
    navigateTo('/')
}

async function updateUser() {
    const payload = {
        name: state.user.name,
        course: state.user.course,
        email: state.user.email,
        password: state.user.password,
        is_active: state.user.is_active,
    }
    await $fetch(`http://127.0.0.1:8000/api/users/${userId}`, {
        method: 'PUT',
        body: payload
    }).then((result) => {
        if (result) {
            alert('Successfully updated.')
        }
    }).catch((errors) => {
        state.errors = errors
    })
}
</script> -->
<template>
    <div class="mx-auto max-w-5xl py-10">
        <h3 class="text-2xl">Edit User</h3>
        <div class="py-3">
            <button @click="back()" class="border px-4 py-1 hover:bg-gray-50">Back</button>
        </div>
        <div v-if="pending">
            Loading...
        </div>
        <div v-else>
            <form class="space-y-3" @submit.prevent="updateUser()">
                <div>
                    <FormLabel label="Name" />
                    <FormTextField name="name" placeholder="Name" v-model="state.user.name" />
                    <div>
                        {{ state.errors && state.errors.data && state.errors.data.errors && state.errors.data.errors.name && state.errors.data.errors.name[0] }}
                    </div>
                </div>
                <div>
                    <FormLabel label="Course" />
                    <FormTextField name="course" placeholder="Course" v-model="state.user.course" />
                    <div>
                        {{ state.errors && state.errors.data && state.errors.data.errors && state.errors.data.errors.course && state.errors.data.errors.course[0] }}
                    </div>
                </div>
                <div>
                    <FormLabel label="Email" />
                    <FormTextField name="email" placeholder="email" v-model="state.user.email" />
                    <div>
                        {{ state.errors && state.errors.data && state.errors.data.errors && state.errors.data.errors.email && state.errors.data.errors.email[0] }}
                    </div>
                </div>
                <div>
                    <FormLabel label="Password" />
                    <div class="relative">
                        <FormTextField
                            :type="showPassword ? 'text' : 'password'"
                            name="password"
                            placeholder="password"
                            v-model="state.user.password"
                        />
                        <button
                            type="button"
                            class="absolute top-1/2 right-3 transform -translate-y-1/2 text-gray-500 focus:outline-none"
                            @click="showPassword = !showPassword"
                        >
                            <svg
                                v-if="showPassword"
                                xmlns="http://www.w3.org/2000/svg"
                                viewBox="0 0 24 24"
                                fill="none"
                                stroke="currentColor"
                                stroke-width="2"
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                class="w-5 h-5"
                            >
                                <path d="M22.617 4.617a9 9 0 0 0-12.718 0L12 5.828l-1.899-1.9a9 9 0 0 0-2.618 2.616L12 10.061l4.516-4.516a9 9 0 0 0 2.101 2.616L12 14.172l-1.899-1.9a9 9 0 0 0 2.101-2.616L12 10.06l1.899 1.9a9 9 0 0 0 2.618-2.616L12 5.828l1.899-1.9a9 9 0 0 0 2.718 2.617z" />
                                <circle cx="12" cy="12" r="3" />
                            </svg>
                            <svg
                                v-else
                                xmlns="http://www.w3.org/2000/svg"
                                viewBox="0 0 24 24"
                                fill="none"
                                stroke="currentColor"
                                stroke-width="2"
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                class="w-5 h-5"
                            >
                                <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 1 21 12.79z" />
                            </svg>
                        </button>
                    </div>
                    <div>
                        {{ state.errors && state.errors.data && state.errors.data.errors && state.errors.data.errors.password && state.errors.data.errors.password[0] }}
                    </div>
                </div>
                <div>
                    <FormLabel label="Status" />
                    <br />
                    <FormCheckbox :value="state.user.is_active ? true : false"
                        @click="state.user.is_active = !state.user.is_active" />
                </div>
                <div>
                    <FormButton type="submit" buttonStyle="primary" class="w-full">Update</FormButton>
                </div>
            </form>
        </div>
    </div>
</template>

<script setup>
import { ref, reactive, watch } from 'vue';

const route = useRoute();
const userId = route.query.user_id;
const showPassword = ref(false);

const { pending, data: user } = await useLazyAsyncData('user', () => $fetch(`http://127.0.0.1:8000/api/users/${userId}`))

const state = reactive({
    user: {
        name: user && user.value && user.value.name,
        course: user && user.value && user.value.course,
        email: user && user.value && user.value.email,
        password: user && user.value && user.value.password,
        is_active: user && user.value && user.value.is_active,
    }
})

watch(user, (newData) => {
    state.user = {
        name: newData && newData.name,
        course: newData && newData.course,
        email: newData && newData.email,
        password: newData && newData.password,
        is_active: newData && newData.is_active,
    }
})

function back() {
    navigateTo('/')
}

async function updateUser() {
    const payload = {
        name: state.user.name,
        course: state.user.course,
        email: state.user.email,
        password: state.user.password,
        is_active: state.user.is_active,
    }
    await $fetch(`http://127.0.0.1:8000/api/users/${userId}`, {
        method: 'PUT',
        body: payload
    }).then((result) => {
        if (result) {
            alert('Successfully updated.')
        }
    }).catch((errors) => {
        state.errors = errors
    })
}
</script>
