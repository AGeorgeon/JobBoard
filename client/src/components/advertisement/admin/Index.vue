<template>
  <div>
    <Navigation />
    <!-- Search -->
    <section>
      <div class="container">
        <h1>advertisement</h1>
      </div>
    </section>

    <br />

    <!-- Content -->
    <section>
      <div class="container">
        <div class="card">
          <table class="highlight centered">
            <thead>
              <tr>
                <th>Name</th>
                <th>Status</th>
                <th>Action(s)</th>
              </tr>
            </thead>

            <tbody>
              <tr v-for="advertisement in advertisements" :key="advertisement._id">
                <td>{{ advertisement.name }}</td>
                <td>
                  <span
                    v-if="advertisement.isActive || advertisement.isActive==null"
                    class="new badge"
                    data-badge-caption="ACTIVE"
                  ></span>
                  <span
                    v-if="advertisement.isActive == false"
                    class="new badge red"
                    data-badge-caption="INACTIVE"
                  ></span>
                </td>
                <!-- Button -->
                <td>
                  <span>
                    <a
                      :href="edit_advertisement_url + advertisement._id"
                      class="btn-floating amber accent-4"
                      ><i class="material-icons">build</i></a
                    >
                  </span>
                  <span>
                    <button
                      class="btn-floating red darken-1"
                      @click.prevent="deleteThis(advertisement._id)"
                    >
                      <i class="material-icons">delete</i>
                    </button>
                  </span>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import Navigation from "../../partials/Admin_Navigation";
import axios from "axios";

export default {
  components: {
    Navigation,
  },
  data() {
    return {
      show_advertisement_url: "http://localhost:8080/admin/advertisement/show/",
      edit_advertisement_url: "http://localhost:8080/admin/advertisement/edit/",
      delete_advertisement_url: "http://localhost:8080/admin/advertisement/delete/",
      advertisements: null,
      name: null,
      description: null,
    };
  },
  mounted() {
    this.search();
  },
  methods: {
    search: function () {
      axios
        .post("http://localhost:8081/advertisement/search", {
          name: this.name,
        })
        .then(
          (response) => (
            (this.advertisements = response.data), console.log(response.data)
          )
        );
    },
    deleteThis: function (deleteId) {
      console.log("test " + deleteId);
      axios
        .delete(`http://localhost:8081/advertisement/${deleteId}`)
        .then((response) => ((this.advertisements = response.data), this.search()));
    },
  },
};
</script>

<style>
</style>