<script>
import { mapActions, mapWritableState } from "pinia";

import { RouterLink } from "vue-router";
import { main } from "../stores/counter";
export default {
  name: `NavBar`,
  components: { RouterLink },
  methods: {
    ...mapActions(main, ["logout"]),
    handleLogout() {
      this.logout();
    },
  },
  computed: { ...mapWritableState(main, ["isLoggedIn", "isHome"]) },
};
</script>

<template>
  <nav
    class="font-sans flex flex-col text-center sm:flex-row sm:text-left sm:justify-between py-4 px-6 bg-white shadow sm:items-baseline w-full"
  >
    <div class="mb-2 sm:mb-0">
      <RouterLink
        class="font-bold text-xl no-underline text-grey-darkest hover:text-blue-dark ml-2"
        to="/"
        >Home</RouterLink
      >
      <a
        href="/profile"
        class="text-lg no-underline text-grey-darkest hover:text-blue-dark ml-4"
        >Your Profile</a
      >
      <a
        href="/shoppingcart"
        class="text-lg no-underline text-grey-darkest hover:text-blue-dark ml-4"
        >Shopping Cart</a
      >
      <RouterLink
        v-if="!isLoggedIn"
        class="text-lg no-underline text-grey-darkest hover:text-blue-dark ml-2"
        to="/login"
        >Login</RouterLink
      >
      <a
        v-if="isLoggedIn"
        v-on:click="logout"
        class="text-lg no-underline text-red-darkest hover:text-blue-dark ml-4"
        >Logout</a
      >
    </div>
    <div>
      <form>
        <label
          for="default-search"
          class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-gray-300"
          >Search</label
        >
        <div v-if="isHome" class="relative">
          <div
            class="flex absolute inset-y-0 left-0 items-center pl-3 pointer-events-none"
          >
            <svg
              aria-hidden="true"
              class="w-5 h-5 text-gray-500 dark:text-gray-400"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
              ></path>
            </svg>
          </div>
          <input
            type="search"
            id="default-search"
            class="block p-4 pl-10 w-full text-sm text-gray-900 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:border-gray-600 dark:placeholder-gray-400 dark:text-black dark:focus:ring-blue-500 dark:focus:border-blue-500"
            placeholder="Search..."
            required
          />
          <button
            type="submit"
            class="text-white absolute right-2.5 bottom-2.5 bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-4 py-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
          >
            Search
          </button>
        </div>
      </form>
    </div>
  </nav>
</template>
