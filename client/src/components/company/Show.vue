<template>
  <div>
    <Navigation />

    <div class="container" style="margin-bottom: 150px;">
    <div class="col s12 m12 l9">
      	<h3 class="center">{{ title }}</h3>
      	<div class="row">
        	<div class="col s12">
        	  <div class="card">
        	    <section id="grid">
        	      <div class="box">
        	        <div class="box-content box-titre">
        	          <h1 class="center">{{ company.name }}</h1>
        	        </div>
                  <div class="card-content">
                    <p>{{ company.description }}</p>
                    <a :href="url + company._id">Create Ads</a>
              </div>
        	      </div>

        	      <div class="box">
        	        <div class="box-content box-info">
        	          <ul class="collection with-header tab">
        	            <h3>{{ company.name }} Advertisement:</h3>
                      <div v-for="advertisement in advertisements" :key="advertisement._id">
                        <div class="col s6">
                          <div class="card">
                            <div class="card-content">
                              <span class="card-title">{{ advertisement.name }}</span>
                              <!-- TODO DESCRIPTION WITH TRUNCATE -->
                            </div>
                            <div class="card-action center">
                              <div v-if="isLoggedIn">
                                <a :href="candidacy_url_create + advertisement._id"
                                  >Apply</a
                                >
                              </div>
                            </div>
                          </div>
                        </div>
                      </div>
        	          </ul>
        	        </div>
        	      </div>
        	    </section>
        	  </div>
        	</div>
      	</div>
    </div>
  </div>
  </div>
</template>


<!--------------------------------------------------	JS	------------------------------------->
<script>
import axios from "axios";
import Navigation from "../partials/Navigation";

export default {
  title: "Company Show",
  props: ["id"],
  data() {
    return {
      company: null,
      advertisements: null,
      url: "http://localhost:8080/advertisement/create/",
      candidacy_url_create: "http://localhost:8080/candidacy/create/",
    };
  },
  mounted() {
    axios({
      url: `http://localhost:8081/company/${this.id}`,
      method: "get",
    }).then((response) => (this.company = response.data));

    axios({
      url: `http://localhost:8081/advertisement/company/${this.id}`,
      method: "get",
    }).then((response) => (this.advertisements = response.data));
  },
  components: {
    Navigation,
  },
};
</script>



<!--------------------------------------------------	CSS	------------------------------------->
<style scoped>
main {
  width: 100%;
  display: flex;
  justify-content: space-around;
}

.page {
  display: flex;
  justify-content: center;
}

section {
  width: 100%;
  height: 100vh;
  max-height: 700px;
  background-color: black;
  color: white;
}

#grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(3, 1fr);
  width: 100%;
}

.box {
  display: flex;
  align-items: center;
  padding: 0;
  margin: 0;
}
.box-content {
  width: 100%;
}
.box-info {
  width: 100%;
  margin: 0;
  padding: 0;
}

.box-titre {
  text-align: left;
  padding-left: 50px;
}

.box:nth-child(1) {
  background-color: #008c9e;
  grid-column-start: 1;
  grid-column-end: 4;
  grid-row-start: 1;
  grid-row-end: 2;
  text-align: center;
}
.box:nth-child(2) {
  background-color: white;
  padding-left: 40px;
  color: black;
  grid-column-start: 1;
  grid-column-end: 4;
  grid-row-start: 2;
  grid-row-end: 4;
}

ul {
  margin-right: 9%;
}

.centrer {
  display: flex;
  justify-content: center !important;
}
.card {
  width: 100%;
}
</style>
