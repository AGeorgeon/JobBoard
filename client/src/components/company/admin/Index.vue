<template>
  <div>
    <Navigation />
    <!-- Search -->
    <section>
      <div class="container">
        <h1>Company</h1>
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
                <th>Country</th>
                <th>Size</th>
                <th>Status</th>
                <th>Action(s)</th>
              </tr>
            </thead>

            <tbody>
              <tr v-for="company in companies" :key="company._id">
                <td>{{ company.name }}</td>
                <td>{{ company.country }}</td>
                <td>
                  <span
                    v-if="company.size == TPE"
                    class="new badge"
                    data-badge-caption="TPE"
                  ></span>
                  <span
                    v-if="company.size == PE"
                    class="new badge"
                    data-badge-caption="PE"
                  ></span>
                  <span
                    v-if="company.size == ME"
                    class="new badge"
                    data-badge-caption="ME"
                  ></span>
                  <span
                    v-if="company.size == ETI"
                    class="new badge"
                    data-badge-caption="ETI"
                  ></span>
                  <span
                    v-if="company.size == GE"
                    class="new badge"
                    data-badge-caption="GE"
                  ></span>
                  <span
                    v-if="company.size == null"
                    class="new badge"
                    data-badge-caption="NONE"
                  ></span>
                </td>
                <td>
                  <span
                    v-if="company.isActive == true"
                    class="new badge"
                    data-badge-caption="ACTIVE"
                  ></span>
                  <span
                    v-if="company.isActive == false"
                    class="new badge red"
                    data-badge-caption="INACTIVE"
                  ></span>
                </td>
                <!-- Button -->
                <td>
                  <span>
                    <a
                      :href="edit_company_url + company._id"
                      class="btn-floating amber accent-4"
                      ><i class="material-icons">build</i></a
                    >
                  </span>
                  <span>
                    <button
                      class="btn-floating red darken-1"
                      @click.prevent="deleteThis(company._id)"
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
      show_company_url: "http://localhost:8080/admin/company/show/",
      edit_company_url: "http://localhost:8080/admin/company/edit/",
      delete_company_url: "http://localhost:8080/admin/company/delete/",
      companies: null,
      name: null,
      country: null,
      description: null,
      size: null,
    };
  },
  mounted() {
    this.search();
  },
  methods: {
    search: function () {
      axios
        .post("http://localhost:8081/company/search", {
          name: this.name,
        })
        .then(
          (response) => (
            (this.companies = response.data), console.log(response.data)
          )
        );
    },
    deleteThis: function (deleteId) {
      console.log("test " + deleteId);
      axios
        .delete(`http://localhost:8081/company/${deleteId}`)
        .then((response) => ((this.companies = response.data), this.search()));
    },
  },
};
</script>

<style>
</style>