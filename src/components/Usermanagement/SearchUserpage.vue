<template>
  <div>
    <form class="md:flex hidden flex-row flex-wrap items-center lg:ml-auto mr-3">
      <div class="relative flex w-full flex-wrap items-stretch">
        <span
          class="z-10 h-full leading-snug font-normal absolute text-center text-blueGray-300 absolute bg-transparent rounded text-base items-center justify-center w-8 pl-3 py-3"
        >
          <i class="fas fa-search"></i>
        </span>
        <input
          type="text"
          class="border-0 px-3 py-3 placeholder-blueGray-300 text-blueGray-600 relative bg-white bg-white rounded text-sm shadow outline-none focus:outline-none focus:ring w-full pl-10"
          id="name"
          required
          v-model="name"
          name="name"
        />
      </div>

      <div class="btn-group">
        <button @click="searchUsers" class="btn btn-success">Search</button>
      </div>
    </form>

    <ul class="search-result">
      <li v-for="user in users" :key="user.id">
        <h6>({{ user.name }}) ({{ user.email }})</h6>
        <!-- Display other user details here -->
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios"
export default {
  name: "SearchUser",
  data() {
    return {
      name: "",
      users: [],
    };
  },
  methods: {
    searchUsers() {
      axios
        .get("http://localhost:3303/api/v1/user", {
          params: { name: this.name },
        })
        .then((response) => {
          this.users = response.data;
          console.log(response.data);
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>
