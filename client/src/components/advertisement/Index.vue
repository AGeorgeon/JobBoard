<template>
  <div>
    <Navigation />
    <div class="container">
      <div class="row">
        <div class="col s12">
          <div class="card">
            <div class="card-content">
              <h1 class="center">Advertisement</h1>
                <ul class="collapsible">
                  <li>
                    <div class="collapsible-header"><i class="material-icons">search</i>Filter</div>
              <div class="collapsible-body">
              <section>
                <form action="" method="post">
                  <div>
                    <label for="name">Name</label>
                    <input type="text" name="name" id="name" v-model="name" />
                  </div>
                  <div class="input-field col s12">
                    <label for="contract_type">Contract Type</label>
                    <select name="contract_type" id="contract_type" v-model="contract_type">
                      <option value="" disabled selected></option>
                      <option value="">All</option>
                      <option value="CDI">CDI</option>
                      <option value="CDD">CDD</option>
                      <option value="CTT">CTT</option>
                      <option value="CUI">CUI</option>
                      <option value="CAE">CAE</option>
                      <option value="CIE">CIE</option>
                    </select>
                  </div>
                  <div class="input-field col s12">
                    <label for="education">Education</label>
                    <select name="education" id="education" v-model="education">
                      <option value="" disabled selected></option>
                      <option value="">All</option>
                      <option value="1">Step 1</option>
                      <option value="2">Step 2</option>
                      <option value="3">CAP, BEP</option>
                      <option value="4">Bac</option>
                      <option value="5">BTS, DUT</option>
                      <option value="6">Licence</option>
                      <option value="7">Master</option>
                      <option value="8">Doctoral</option>
                    </select>
                  </div>
                  <div class="input-field col s12">
                    <label for="remote">Remote</label>
                    <select name="remote" id="remote" v-model="remote">
                      <option value="" disabled selected></option>
                      <option value="">All</option>
                      <option value="unremote">Unremote</option>
                      <option value="partially_remote">Partially remote</option>
                      <option value="distributed_team">Distributed team</option>
                      <option value="full_remote">Full remote</option>
                    </select>
                  </div>
                  <div class="input-field col s12">
                    <label for="language">Language</label>
                    <select name="language" id="language" v-model="language">
                      <option value="" disabled selected></option>
                      <option value="">All</option>
                      <option value="en">English</option>
                      <option value="fr">French</option>
                      <option value="de">German</option>
                      <option value="it">Italian</option>
                    </select>
                  </div>
                  <div>
                    <button class="btn" type="submit" @click.prevent="search()">
                      Search
                    </button>
                  </div>
                </form>
              </section>
              </div>
                  </li>
                </ul>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="container">
      <div class="row">
        <div v-for="advertisement in advertisements" :key="advertisement._id">
          <div class="col s6">
            <div class="card">
              <div class="card-content">
                <span class="card-title">{{ advertisement.name }}</span>
                <!-- TODO DESCRIPTION WITH TRUNCATE -->
                {{ advertisement.description }}
              </div>
              <div class="card-action center">
                <a class="btn couleur" :href="candidacy_url_create + advertisement._id">Apply</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navigation from "../partials/Navigation";
import axios from "axios";

export default {
  data() {
    return {
      advertisements: null,
      advertisement_url_show: "http://localhost:8080/advertisement/show/",
      candidacy_url_create: "http://localhost:8080/candidacy/create/",
      name: null,
      contract_type: null,
      education: null,
      remote: null,
      language: null,
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
          contract_type: this.contract_type,
          education: this.education,
          remote: this.remote,
          language: this.language,
        })
        .then((response) => (this.advertisements = response.data));
    },
  },
  components: {
    Navigation,
  },
};
</script>

<style>
.couleur{
  background-color: #938B76  !important;
}
.btn{
  background-color: #938B76  !important;
}
</style>