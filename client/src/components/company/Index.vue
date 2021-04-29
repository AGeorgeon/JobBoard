<template>
  <div>
    <Navigation />
    <div>
      <div class="row">
        <div class="col s12" style="margin-bottom: 100px">
          <div class="section">
          <h1 class="">Companies</h1>
            <!-------------------------------------------------->
            <div class="col s12 m6 l4" v-for="company in companies" :key="company._id">
              <div class="card">
                <div class="card-content backIcon">
                  <div class="box-titre">
                    <h4> {{ company.name }} </h4>
                    <btn :href="company_url + company._id" class="btn couleurBouton" >Seen Company</btn>
                  </div>
                </div>
              </div>
            </div>
            <!-------------------------------------------------->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Navigation from "../partials/Navigation";

export default {
  data() {
    return {
      companies: null,
      company_url: "http://localhost:8080/company/show/",
    };
  },
  mounted() {
    axios
      .get("http://localhost:8081/company")
      .then((response) => (this.companies = response.data));
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

.couleurBouton{
  background-color: #938B76 !important;
}
.backIcon{
  background-color: #D7CEB2 !important;
}

#grid {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  grid-template-rows: repeat(1, 1fr);
  width: 100%;
}

.box-titre {
  text-align: left;
  padding-left: 50px;
}

ul {
  margin-right: 9%;
}
a{
  color: black;
}
</style>