<template>
  <div>
    <Navigation />
    <!-- Search -->
    <section>
      <div class="container">
        <h1>candidacy</h1>
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
                <th>Username</th>
                <th>Status</th>
                <th>Action(s)</th>
              </tr>
            </thead>

            <tbody>
              <tr v-for="candidacy in candidacies" :key="candidacy._id">
                <td v-if="candidacy.people">{{ candidacy.people.firstname }} {{ candidacy.people.lastname }}</td>
                <td v-if="!candidacy.people">Anonymous</td>
                <td>
                  <span
                    v-if="candidacy.isActive || candidacy.isActive==null"
                    class="new badge"
                    data-badge-caption="ACTIVE"
                  ></span>
                  <span
                    v-if="candidacy.isActive == false"
                    class="new badge red"
                    data-badge-caption="INACTIVE"
                  ></span>
                </td>
                <!-- Button -->
                <td>
                  <span>
                    <button
                      class="btn-floating red darken-1"
                      @click.prevent="deleteThis(candidacy._id)"
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
      show_candidacy_url: "http://localhost:8080/admin/candidacy/show/",
      edit_candidacy_url: "http://localhost:8080/admin/candidacy/edit/",
      delete_candidacy_url: "http://localhost:8080/admin/candidacy/delete/",
      candidacies: null,
      description: null,
    };
  },
  mounted() {
    this.search();
  },
  methods: {
    search: function () {
      axios
        .get("http://localhost:8081/candidacy", {
        })
        .then(
          (response) => (
            (this.candidacies = response.data), console.log(response.data)
          )
        );
    },
    deleteThis: function (deleteId) {
      console.log("test " + deleteId);
      axios
        .delete(`http://localhost:8081/candidacy/${deleteId}`)
        .then((response) => ((this.candidacies = response.data), this.search()));
    },
  },
};
</script>

<style>
</style>