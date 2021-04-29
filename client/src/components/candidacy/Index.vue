<!--<template>
  <div>
    <Navigation />

    <h1>Index</h1>

    <ul id="example-1">
      <li v-for="candidacy in candidacies" :key="candidacy._id">
        {{ candidacy }}
      </li>
    </ul>
  </div>
</template>-->

<template>
  <div>
    <Navigation />
    <div>
      <div class="row">
        <div class="col s12" style="margin-bottom: 100px">
          <div class="section">
          <h1 class="">Candidacy</h1>
            <!-------------------------------------------------->
            <div class="col s12 m6 l4" v-for="candidacy in candidacies" :key="candidacy._id">
              <div class="card teal">
                <div class="card-image waves-effect waves-block waves-light">
                  <section id="grid">
                    <div class="box">
                      <div class="box-content box-titre">
                        <h4 class="white-text"> {{ candidacy.description }} </h4>
                        <!-- TODO Faire une redirection vers le show ou on voit l'annonce en grand -->
                      </div>
                    </div>
                  </section>
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
import Navigation from "../partials/Navigation";
import axios from "axios";

export default {
  data() {
    return {
      candidacies: null,
    };
  },
  mounted() {
    axios
      .get("http://localhost:8081/candidacy")
      .then((response) => (this.candidacies = response.data));
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
  max-width: 862px;
  height: 18vh;
  max-height: 500px;
  background-color: black;
  color: white;
}

#grid {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  grid-template-rows: repeat(1, 1fr);
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
  background-color: #a59e8c;
  grid-column-start: 1;
  grid-column-end: 4;
  grid-row-start: 1;
  grid-row-end: 1;
  text-align: center;
}


ul {
  margin-right: 9%;
}
a{
  color: black;
}
</style>