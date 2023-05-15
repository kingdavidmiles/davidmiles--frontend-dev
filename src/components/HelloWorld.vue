<template>
  <div class="container-xxl">
    <div class="fw-bold pb-5">
      All the card items listed are real data fetched from the server. You can click on any card to copy all the information within it, including the name, email, address, zipcode, phone number, website, and company details.
    </div>
    <div class="row">
      <div class="col-md-4 col-xs-12" v-for="(user, index) in users" :key="index">
        <div>
          <!-- listing all the card from the server -->
          <b-card
            class="my-3 text text-capitalize shadow-lg"
            style="border-color: transparent"
            @click="copyText(user)"
          >
            <b-card-text>
              name: &nbsp;{{ user.name }} {{ user.username }}
            </b-card-text>

            <b-card-text>email: &nbsp; {{ user.email }}</b-card-text>
            <b-card-text>address: &nbsp; {{ user.address.street }}</b-card-text>
            <b-card-text>zipcode: &nbsp;{{ user.address.zipcode }}</b-card-text>
            <b-card-text>phone: &nbsp;{{ user.phone }}</b-card-text>
            <b-card-text>website:&nbsp; {{ user.website }}</b-card-text>
            <b-card-text>company: &nbsp;{{ user.company.name }}</b-card-text>
          </b-card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Swal from "sweetalert2";
export default {
  name: "HelloWorld",
  data() {
    return {
      apiUrl: "https://jsonplaceholder.typicode.com/users",
      users: [],
    };
  },
  methods: {
    copyText(user) {
      const text =
        `name: ${user.name} ${user.username}\n` +
        `email: ${user.email}\n` +
        `address: ${user.address.street}\n` +
        `zipcode: ${user.address.zipcode}\n` +
        `phone: ${user.phone}\n` +
        `website: ${user.website}\n` +
        `company: ${user.company.name}`;

      navigator.clipboard
        .writeText(text)
        .then(() => {
          console.log("Text copied to clipboard:", text);
          Swal.fire({
            position: "center",
            icon: "success",
            title: "Card information copied successfully",
            showConfirmButton: false,
            timer: 1500,
          });
        })
        .catch((error) => {
          console.error("Error copying text to clipboard:", error);
        });
    },
  },
  mounted() {
    axios
      .get(this.apiUrl)
      .then((response) => {
        this.users = response.data;
        console.log("API response:", this.posts);
      })
      .catch((error) => {
        console.error("Error fetching API data:", error);
      });
  },
};
</script>

<style scoped>
.text {
  text-align: left;
}
</style>
