<script setup>
import { Head, Link, useForm } from "@inertiajs/vue3";
import AuthenticationCard from "@/Components/AuthenticationCard.vue";
import AuthenticationCardLogo from "@/Components/AuthenticationCardLogo.vue";
import Checkbox from "@/Components/Checkbox.vue";
import InputError from "@/Components/InputError.vue";
import InputLabel from "@/Components/InputLabel.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import TextInput from "@/Components/TextInput.vue";

const form = useForm({
    first_name: "",
    owner_name: "",
    last_name: "",
    phone: "",
    role: "owner",
    email: "",
    password: "",
    password_confirmation: "",
    terms: false,
});

const submit = () => {
    form.post(route("register"), {
        onFinish: () => form.reset("password", "password_confirmation"),
        onError: (err) => {
            console.log(err);
        },
    });
};
</script>

<template>
    <Head title="Register" />

    <section class="bg-white dark:bg-gray-900">
        <div class="flex justify-center min-h-screen">
            <div
                class="hidden bg-cover lg:block lg:w-2/5"
                style="
                    background-image: url('https://images.unsplash.com/photo-1494621930069-4fd4b2e24a11?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=715&q=80');
                "
            ></div>

            <div
                class="flex items-center w-full max-w-3xl p-8 mx-auto lg:px-12 lg:w-3/5"
            >
                <div class="w-full">
                    <h1
                        class="text-2xl font-semibold tracking-wider text-gray-800 capitalize dark:text-white"
                    >
                        Get your free account now.
                    </h1>

                    <p class="mt-4 text-gray-500 dark:text-gray-400">
                        Let’s get you all set up so you can verify your personal
                        account and begin setting up your profile.
                    </p>

                    <div class="mt-6">
                        <h1 class="text-gray-500 dark:text-gray-300">
                            Select type of account
                        </h1>

                        <div class="mt-3 md:flex md:items-center md:-mx-2">
                            <button
                                type="button"
                                @click="form.role = 'owner'"
                                :class="{
                                    'text-white bg-blue-500':
                                        form.role === 'owner',
                                    'border text-blue-500 border-blue-500':
                                        form.role !== 'owner',
                                }"
                                class="flex justify-center w-full px-6 py-3 rounded-lg md:w-auto md:mx-2 focus:outline-none"
                            >
                                <svg
                                    xmlns="http://www.w3.org/2000/svg"
                                    class="w-6 h-6"
                                    fill="none"
                                    viewBox="0 0 24 24"
                                    stroke="currentColor"
                                    stroke-width="2"
                                >
                                    <path
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                                    />
                                </svg>

                                <span class="mx-2"> Owner </span>
                            </button>

                            <button
                                type="button"
                                @click="form.role = 'buyer'"
                                :class="{
                                    'text-white bg-blue-500':
                                        form.role === 'buyer',
                                    'border text-blue-500 border-blue-500':
                                        form.role !== 'buyer',
                                }"
                                class="flex justify-center w-full px-6 py-3 mt-4 rounded-lg md:mt-0 md:w-auto md:mx-2 focus:outline-none"
                            >
                                <svg
                                    xmlns="http://www.w3.org/2000/svg"
                                    class="w-6 h-6"
                                    fill="none"
                                    viewBox="0 0 24 24"
                                    stroke="currentColor"
                                    stroke-width="2"
                                >
                                    <path
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
                                    />
                                </svg>

                                <span class="mx-2"> Buyer </span>
                            </button>
                        </div>
                        <InputError
                            class="mt-2"
                            :message="form.errors.owner_name"
                        />
                    </div>

                    <form
                        @submit.prevent="submit"
                        class="grid grid-cols-1 gap-6 mt-8 md:grid-cols-2"
                    >
                        <div v-if="form.role === 'owner'" class="col-span-2">
                            <label
                                class="block mb-2 text-sm text-gray-600 dark:text-gray-200"
                                >Owner Name</label
                            >
                            <input
                                v-model="form.owner_name"
                                required
                                type="text"
                                placeholder="John"
                                class="block w-full px-5 py-3 mt-2 text-gray-700 placeholder-gray-400 bg-white border border-gray-200 rounded-lg dark:placeholder-gray-600 dark:bg-gray-900 dark:text-gray-300 dark:border-gray-700 focus:border-blue-400 dark:focus:border-blue-400 focus:ring-blue-400 focus:outline-none focus:ring focus:ring-opacity-40"
                            />
                            <InputError
                                class="mt-2"
                                :message="form.errors.first_name"
                            />
                        </div>
                        <div>
                            <label
                                class="block mb-2 text-sm text-gray-600 dark:text-gray-200"
                                >First Name</label
                            >
                            <input
                                v-model="form.first_name"
                                required
                                type="text"
                                placeholder="John"
                                class="block w-full px-5 py-3 mt-2 text-gray-700 placeholder-gray-400 bg-white border border-gray-200 rounded-lg dark:placeholder-gray-600 dark:bg-gray-900 dark:text-gray-300 dark:border-gray-700 focus:border-blue-400 dark:focus:border-blue-400 focus:ring-blue-400 focus:outline-none focus:ring focus:ring-opacity-40"
                            />
                            <InputError
                                class="mt-2"
                                :message="form.errors.first_name"
                            />
                        </div>

                        <div>
                            <label
                                class="block mb-2 text-sm text-gray-600 dark:text-gray-200"
                                >Last name</label
                            >
                            <input
                                v-model="form.last_name"
                                required
                                type="text"
                                placeholder="Snow"
                                class="block w-full px-5 py-3 mt-2 text-gray-700 placeholder-gray-400 bg-white border border-gray-200 rounded-lg dark:placeholder-gray-600 dark:bg-gray-900 dark:text-gray-300 dark:border-gray-700 focus:border-blue-400 dark:focus:border-blue-400 focus:ring-blue-400 focus:outline-none focus:ring focus:ring-opacity-40"
                            />
                            <InputError
                                class="mt-2"
                                :message="form.errors.last_name"
                            />
                        </div>

                        <div>
                            <label
                                class="block mb-2 text-sm text-gray-600 dark:text-gray-200"
                                >Phone number</label
                            >
                            <input
                                v-model="form.phone"
                                type="text"
                                required
                                placeholder="XXX-XX-XXXX-XXX"
                                class="block w-full px-5 py-3 mt-2 text-gray-700 placeholder-gray-400 bg-white border border-gray-200 rounded-lg dark:placeholder-gray-600 dark:bg-gray-900 dark:text-gray-300 dark:border-gray-700 focus:border-blue-400 dark:focus:border-blue-400 focus:ring-blue-400 focus:outline-none focus:ring focus:ring-opacity-40"
                            />
                            <InputError
                                class="mt-2"
                                :message="form.errors.phone"
                            />
                        </div>

                        <div>
                            <label
                                class="block mb-2 text-sm text-gray-600 dark:text-gray-200"
                                >Email address</label
                            >
                            <input
                                v-model="form.email"
                                type="email"
                                placeholder="johnsnow@example.com"
                                class="block w-full px-5 py-3 mt-2 text-gray-700 placeholder-gray-400 bg-white border border-gray-200 rounded-lg dark:placeholder-gray-600 dark:bg-gray-900 dark:text-gray-300 dark:border-gray-700 focus:border-blue-400 dark:focus:border-blue-400 focus:ring-blue-400 focus:outline-none focus:ring focus:ring-opacity-40"
                            />
                            <InputError
                                class="mt-2"
                                :message="form.errors.email"
                            />
                        </div>

                        <div>
                            <label
                                class="block mb-2 text-sm text-gray-600 dark:text-gray-200"
                                >Password</label
                            >
                            <input
                                v-model="form.password"
                                type="password"
                                placeholder="Enter your password"
                                class="block w-full px-5 py-3 mt-2 text-gray-700 placeholder-gray-400 bg-white border border-gray-200 rounded-lg dark:placeholder-gray-600 dark:bg-gray-900 dark:text-gray-300 dark:border-gray-700 focus:border-blue-400 dark:focus:border-blue-400 focus:ring-blue-400 focus:outline-none focus:ring focus:ring-opacity-40"
                            />
                            <InputError
                                class="mt-2"
                                :message="form.errors.password"
                            />
                        </div>

                        <div>
                            <label
                                class="block mb-2 text-sm text-gray-600 dark:text-gray-200"
                                >Confirm password</label
                            >
                            <input
                                v-model="form.password_confirmation"
                                type="password"
                                placeholder="Enter your password"
                                class="block w-full px-5 py-3 mt-2 text-gray-700 placeholder-gray-400 bg-white border border-gray-200 rounded-lg dark:placeholder-gray-600 dark:bg-gray-900 dark:text-gray-300 dark:border-gray-700 focus:border-blue-400 dark:focus:border-blue-400 focus:ring-blue-400 focus:outline-none focus:ring focus:ring-opacity-40"
                            />
                            <InputError
                                class="mt-2"
                                :message="form.errors.password_confirmation"
                            />
                        </div>

                        <button
                            class="flex items-center justify-between w-full px-6 py-3 text-sm tracking-wide text-white capitalize transition-colors duration-300 transform bg-blue-500 rounded-lg hover:bg-blue-400 focus:outline-none focus:ring focus:ring-blue-300 focus:ring-opacity-50"
                        >
                            <span>Sign Up </span>

                            <svg
                                xmlns="http://www.w3.org/2000/svg"
                                class="w-5 h-5 rtl:-scale-x-100"
                                viewBox="0 0 20 20"
                                fill="currentColor"
                            >
                                <path
                                    fill-rule="evenodd"
                                    d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
                                    clip-rule="evenodd"
                                />
                            </svg>
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </section>

    <!-- <AuthenticationCard>
        <template #logo>
            <AuthenticationCardLogo />
        </template>

        <form @submit.prevent="submit">
            <div class="mt-6">
                <h1 class="text-gray-500 dark:text-gray-300">
                    Select type of account
                </h1>

                <div class="mt-3 md:flex md:items-center md:-mx-2">
                    <button
                        type="button"
                        @click="form.role = 'owner'"
                        :class="{
                            'text-white bg-blue-500': form.role === 'owner',
                            'border text-blue-500 border-blue-500':
                                form.role !== 'owner',
                        }"
                        class="flex justify-center w-full px-6 py-3 rounded-lg md:w-auto md:mx-2 focus:outline-none"
                    >
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="w-6 h-6"
                            fill="none"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                            stroke-width="2"
                        >
                            <path
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                            />
                        </svg>

                        <span class="mx-2"> Owner </span>
                    </button>

                    <button
                        type="button"
                        @click="form.role = 'buyer'"
                        :class="{
                            'text-white bg-blue-500': form.role === 'buyer',
                            'border text-blue-500 border-blue-500':
                                form.role !== 'buyer',
                        }"
                        class="flex justify-center w-full px-6 py-3 mt-4 rounded-lg md:mt-0 md:w-auto md:mx-2 focus:outline-none"
                    >
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="w-6 h-6"
                            fill="none"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                            stroke-width="2"
                        >
                            <path
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"
                            />
                        </svg>

                        <span class="mx-2"> Buyer </span>
                    </button>
                </div>
            </div>

            <div class="mt-4">
                <InputLabel for="name" value="Name" />
                <TextInput
                    id="name"
                    v-model="form.name"
                    type="text"
                    class="mt-1 block w-full"
                    required
                    autofocus
                    autocomplete="name"
                />
                <InputError class="mt-2" :message="form.errors.name" />
            </div>

            <div class="mt-4">
                <InputLabel for="email" value="Email" />
                <TextInput
                    id="email"
                    v-model="form.email"
                    type="email"
                    class="mt-1 block w-full"
                    required
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
                    autocomplete="new-password"
                />
                <InputError class="mt-2" :message="form.errors.password" />
            </div>

            <div class="mt-4">
                <InputLabel
                    for="password_confirmation"
                    value="Confirm Password"
                />
                <TextInput
                    id="password_confirmation"
                    v-model="form.password_confirmation"
                    type="password"
                    class="mt-1 block w-full"
                    required
                    autocomplete="new-password"
                />
                <InputError
                    class="mt-2"
                    :message="form.errors.password_confirmation"
                />
            </div>

            <div
                v-if="$page.props.jetstream.hasTermsAndPrivacyPolicyFeature"
                class="mt-4"
            >
                <InputLabel for="terms">
                    <div class="flex items-center">
                        <Checkbox
                            id="terms"
                            v-model:checked="form.terms"
                            name="terms"
                            required
                        />

                        <div class="ms-2">
                            I agree to the
                            <a
                                target="_blank"
                                :href="route('terms.show')"
                                class="underline text-sm text-gray-600 hover:text-gray-900 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                                >Terms of Service</a
                            >
                            and
                            <a
                                target="_blank"
                                :href="route('policy.show')"
                                class="underline text-sm text-gray-600 hover:text-gray-900 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                                >Privacy Policy</a
                            >
                        </div>
                    </div>
                    <InputError class="mt-2" :message="form.errors.terms" />
                </InputLabel>
            </div>

            <div class="flex items-center justify-end mt-4">
                <Link
                    :href="route('login')"
                    class="underline text-sm text-gray-600 hover:text-gray-900 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                >
                    Already registered?
                </Link>

                <PrimaryButton
                    class="ms-4"
                    :class="{ 'opacity-25': form.processing }"
                    :disabled="form.processing"
                >
                    Register
                </PrimaryButton>
            </div>
        </form>
    </AuthenticationCard> -->
</template>
