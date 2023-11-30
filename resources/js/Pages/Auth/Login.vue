<script setup>
import { Head, Link, useForm } from "@inertiajs/vue3";
import AuthenticationCard from "@/Components/AuthenticationCard.vue";
import AuthenticationCardLogo from "@/Components/AuthenticationCardLogo.vue";
import Checkbox from "@/Components/Checkbox.vue";
import InputError from "@/Components/InputError.vue";
import InputLabel from "@/Components/InputLabel.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import TextInput from "@/Components/TextInput.vue";

defineProps({
    canResetPassword: Boolean,
    status: String,
});

const form = useForm({
    email: "",
    password: "",
    remember: false,
});

const submit = () => {
    form.transform((data) => ({
        ...data,
        remember: form.remember ? "on" : "",
    })).post(route("login"), {
        onFinish: () => form.reset("password"),
    });
};
</script>

<template>
    <Head title="Log in" />

    <AuthenticationCard v-if="false">
        <template #logo>
            <AuthenticationCardLogo />
        </template>

        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
            {{ status }}
        </div>

        <form @submit.prevent="submit">
            <div>
                <InputLabel for="email" value="Email" />
                <TextInput
                    id="email"
                    v-model="form.email"
                    type="email"
                    class="mt-1 block w-full"
                    required
                    autofocus
                    autocomplete="username"
                />
                <InputError class="mt-2" :message="form.errors.email" />
            </div>

            <div class="mt-4">
                <InputLabel for="password" value="Password" />
                <TextInput
                    id="password"
                    v-model="form.password"
                    type="password"
                    class="mt-1 block w-full"
                    required
                    autocomplete="current-password"
                />
                <InputError class="mt-2" :message="form.errors.password" />
            </div>

            <div class="block mt-4">
                <label class="flex items-center">
                    <Checkbox v-model:checked="form.remember" name="remember" />
                    <span class="ms-2 text-sm text-gray-600">Remember me</span>
                </label>
            </div>

            <div class="flex items-center justify-end mt-4">
                <Link
                    v-if="canResetPassword"
                    :href="route('password.request')"
                    class="underline text-sm text-gray-600 hover:text-gray-900 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                >
                    Forgot your password?
                </Link>

                <PrimaryButton
                    class="ms-4"
                    :class="{ 'opacity-25': form.processing }"
                    :disabled="form.processing"
                >
                    Log in
                </PrimaryButton>
            </div>
        </form>
    </AuthenticationCard>

    <div class="bg-white dark:bg-gray-900">
        <div class="flex justify-center h-screen">
            <div
                class="hidden bg-cover lg:block lg:w-2/3"
                style="
                    background-image: url(https://images.unsplash.com/photo-1616763355603-9755a640a287?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80);
                "
            >
                <div
                    class="flex items-center h-full px-20 bg-gray-900 bg-opacity-40"
                >
                    <div>
                        <h2 class="text-2xl font-bold text-white sm:text-3xl">
                            Saseti
                        </h2>

                        <p class="max-w-xl mt-3 text-gray-300">
                            Explore endless possibilities in the realm of real
                            estate with our platform: Empowering Dreams,
                            Building Legacies. Seamlessly connect landowners
                            with eager buyers, making every transaction a step
                            towards forging enduring legacies.
                        </p>
                    </div>
                </div>
            </div>

            <div
                class="flex items-center w-full max-w-md px-6 mx-auto lg:w-2/6"
            >
                <div class="flex-1">
                    <div class="text-center">
                        <div class="flex justify-center mx-auto">
                            <AuthenticationCardLogo />
                        </div>

                        <p class="mt-3 text-gray-500 dark:text-gray-300">
                            Sign in to access your account
                        </p>
                    </div>

                    <div class="mt-8">
                        <form @submit.prevent="submit">
                            <div>
                                <label
                                    for="email"
                                    class="block mb-2 text-sm text-gray-600 dark:text-gray-200"
                                    >Email Address</label
                                >
                                <input
                                    v-model="form.email"
                                    required
                                    autofocus
                                    type="email"
                                    name="email"
                                    id="email"
                                    placeholder="example@example.com"
                                    class="block w-full px-4 py-2 mt-2 text-gray-700 placeholder-gray-400 bg-white border border-gray-200 rounded-lg dark:placeholder-gray-600 dark:bg-gray-900 dark:text-gray-300 dark:border-gray-700 focus:border-blue-400 dark:focus:border-blue-400 focus:ring-blue-400 focus:outline-none focus:ring focus:ring-opacity-40"
                                />
                                <InputError
                                    class="mt-2"
                                    :message="form.errors.email"
                                />
                            </div>

                            <div class="mt-6">
                                <div class="flex justify-between mb-2">
                                    <label
                                        for="password"
                                        class="text-sm text-gray-600 dark:text-gray-200"
                                        >Password</label
                                    >

                                    <Link
                                        v-if="canResetPassword"
                                        :href="route('password.request')"
                                        class="text-sm text-gray-400 focus:text-blue-500 hover:text-blue-500 hover:underline"
                                        >Forgot password?</Link
                                    >
                                </div>

                                <input
                                    v-model="form.password"
                                    required
                                    type="password"
                                    name="password"
                                    id="password"
                                    placeholder="Your Password"
                                    class="block w-full px-4 py-2 mt-2 text-gray-700 placeholder-gray-400 bg-white border border-gray-200 rounded-lg dark:placeholder-gray-600 dark:bg-gray-900 dark:text-gray-300 dark:border-gray-700 focus:border-blue-400 dark:focus:border-blue-400 focus:ring-blue-400 focus:outline-none focus:ring focus:ring-opacity-40"
                                />
                                <InputError
                                    class="mt-2"
                                    :message="form.errors.password"
                                />
                            </div>

                            <div class="block mt-4">
                                <label class="flex items-center">
                                    <Checkbox
                                        v-model:checked="form.remember"
                                        name="remember"
                                    />
                                    <span class="ms-2 text-sm text-gray-400"
                                        >Remember me</span
                                    >
                                </label>
                            </div>

                            <div class="mt-6">
                                <button
                                    class="w-full px-4 py-2 tracking-wide text-white transition-colors duration-300 transform bg-blue-500 rounded-lg hover:bg-blue-400 focus:outline-none focus:bg-blue-400 focus:ring focus:ring-blue-300 focus:ring-opacity-50"
                                >
                                    Sign in
                                </button>
                            </div>
                        </form>

                        <p class="mt-6 text-sm text-center text-gray-400">
                            Don&#x27;t have an account yet?
                            <Link
                                :href="route('register')"
                                href="#"
                                class="text-blue-500 focus:outline-none focus:underline hover:underline"
                                >Sign up</Link
                            >.
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
