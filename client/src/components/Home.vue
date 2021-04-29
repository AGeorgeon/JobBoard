<template>
<body style="margin-bottom: 150px;">
  <div id="app">
    <Navigation />
	<section class="container">
		<section>
			<div class="titre">
				<h1>{{ page_name }} page</h1>
			</div>

			<div>
				<h5 class="titre">Your future is in our hands</h5>
				<nav class="couleur">
					<div class="nav-wrapper">
						<form>
							<div class="input-field">
								<input id="search" type="search" required>
								<label class="label-icon" for="search"><i class="material-icons">search</i></label>
								<i class="material-icons">close</i>
							</div>
						</form>
					</div>
				</nav>
			</div>
		</section>
<!--------------------------------------------------------------------->
		<section>
			<div>
				<h5 class="left-align text">Here are some job postings</h5>
			</div>
		</section>
	</section>
    </div>
</body>
</template>


<!----------------------------------------------------	SCRIPT ----------------------------------------->
<script>
import Navigation from "./partials/Navigation";

export default {

  data() {
    return {
      page_name: "Home",
    };
  },
  components: {
    Navigation,
  },

  mounted() {
    	M.AutoInit();
  }
};
</script>



<!----------------------------------	CSS		------------------------------------->
<!--
Couleur Boutton : #938B76
Couleur Navbar : #A59E8C
-->
<style>
*{
    font-family: 'Poppins', sans-serif;
    padding: 0px;
    margin: 0px;
}


h1{
    font-family: 'Song Myung', serif;
    text-align: center;
    margin: 50px;
}
h5{
    font-family: 'Song Myung', serif;
    text-align: center;
    margin: 50px;
}

.titre{
	display: flex;
	justify-content: center;
}

.text{
	margin: 0px;
	padding-top: 100px;
}

.couleur{
	background-color: #938B76;
}


/***************** Gestion Carousel **************/
.offre{
    display: flex;
    flex-wrap: wrap;
    position: absolute;
}
/*************************************************/

.titreAnnonce{
    text-align: center;
}

</style>