<template>
  <div class="user">
    <div class="user_wrapper">
      <div class="user_wrapper_rechercher">
        <div @click="goToResearch()" class="user_wrapper_rechercher_logo">
          <img src="image/loupe.png" />
        </div>
        <div @click="goToResearch()" class="user_wrapper_rechercher_title">
          Rechercher
        </div>
      </div>
      <div class="user_wrapper_partager">
        <div @click="goToDocument()" class="user_wrapper_partager_logo">
          <img src="image/upload.png" />
        </div>
        <div @click="goToDocument()" class="user_wrapper_partager_title">
          Partager
        </div>
      </div>
    </div>
    <div class="user_content1">
      <div class="user_content1_right">
        <div class="user_content1_right_title">Contact</div>
        <div class="user_content1_right_mail">{{ email }}<br /></div>
      </div>
      <div class="user_content1_left">
        <div class="user_content1_left_desc">
          <h2>{{ nom }} {{ prenom }}</h2>
          <br />
          <h3>Promotion {{ yearPromotion }}</h3>
        </div>
      </div>
      <div class="user_content1_separation"></div>
    </div>
    <div class="user_content2">
      <div class="user_content2_info">
      </div>
    </div>
    <div class="user_content3">
      <div class="user_content3_projet">
        <div class="user_content3_projet_title">Mes projets</div>
        <ul class="liste">
          <li v-if="liste[0] == undefined">Aucun résultat</li>
          <li v-for="item in liste" :key="item.message" class="element">
            {{ item.title }} {{ item.description }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import { me } from "../api/me.js";
import { getProjects } from "../api/getProjects.js";
import router from "../router/index.js";
export default {
  mounted: async function () {
    var infos = await me();
    var projects = await getProjects();
    this.liste = projects.data.informations;

    const informations = infos.data.informations;
    this.nom = informations.name;
    this.prenom = informations.firstname;
    this.email = informations.email;
    this.yearPromotion = informations.yearpromotion;
  },
  data() {
    return {
      nom: "Vous n'êtes pas connecté",
      prenom: "",
      email: "",
      yearPromotion: undefined,
      liste: [],
    };
  },
  methods: {
    goToDocument() {
      router.push("/Document").catch(() => {});
    },
    goToResearch() {
      router.push("/Research").catch(() => {});
    },
  },
};
</script>



<style scoped>
.user {
  width: 100vw;
  height: 80vh;
}
.user_wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row-reverse;
  border: 2px solid #c7c7c7;
  width: 100vw;
  height: 52px;
  font-size: 1em;
}

.user_wrapper_rechercher {
  display: flex;
  flex-direction: row-reverse;
  color: #757575;
  margin: 40px;
}

.user_wrapper_rechercher_logo {
  display: flex;
  justify-content: center;
  height: 35px;
  width: 50px;
}
.user_wrapper_rechercher_title {
  display: flex;
  align-items: center;
  text-transform: uppercase;
}

.user_wrapper_projet {
  display: flex;
  flex-direction: row-reverse;
  color: #757575;
  margin: 40px;
}

.user_wrapper_projet_logo {
  display: flex;
  justify-content: center;
  height: 35px;
  width: 50px;
}

.user_wrapper_projet_title {
  display: flex;
  align-items: center;
  text-transform: uppercase;
}

.user_wrapper_partager {
  display: flex;
  flex-direction: row-reverse;
  color: #757575;
  margin: 40px;
}

.user_wrapper_partager_logo {
  display: flex;
  justify-content: center;
  height: 35px;
  width: 50px;
}

.user_wrapper_partager_title {
  display: flex;
  align-items: center;
  text-transform: uppercase;
}

.user_content1 {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 25vh;
  width: 100vw;
  border-bottom: 2px solid #c7c7c7;
}

.user_content1_left {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row-reverse;
  width: 500px;
}

.user_content1_left_photo {
  display: flex;
  justify-content: center;
  height: 150px;
  width: 150px;
}

.user_content1_left_desc {
  padding-right: 30px;
}

h2 {
  font-weight: bold;
  font-weight: 900;
  font-size: 2.5em;
}

h3 {
  color: #757575;
  font-size: 1.5em;
  font-weight: lighter;
}

.user_content1_separation {
  border-right: 2px solid #c7c7c7;
  display: inline-block;
  height: 130px;
  width: 15vw;
}

.user_content1_right {
  display: flex;
  justify-content: flex-end;
  align-items: flex-start;
  flex-direction: column-reverse;
  height: 120px;
  width: 34vw;
}

.user_content1_right_title {
  font-weight: bold;
  font-weight: 900;
  font-size: 1.5em;
  padding-bottom: 3%;
  line-height: 35px;
}

.user_content1_right_mail {
  text-align: justify;
  color: #757575;
}

.user_content2 {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  height: 15vh;
  width: 100vw;
  border-bottom: 2px solid #c7c7c7;
}

.user_content2_info {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding-left: 5%;
}

.user_content2_info_title {
  font-weight: bold;
  font-weight: 900;
  font-size: 1.5em;
  padding-right: 8%;
}

.user_content2_info_text {
  text-align: left;
  font-style: normal;
  font-weight: normal;
  font-size: 20px;
  color: #757575;
}

.user_content3 {
  height: 40vh;
  width: 100vw;
}


.user_content3_projet_title {
  display: flex;
  justify-content: flex-start;
  padding-left: 5%;
  padding-top: 2%;
  padding-bottom: 2%;
  font-weight: bold;
  font-weight: 900;
  font-size: 1.5em;
}

.user_content3_projet_list {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 50%;
}

.user_content3_projet_list_1_image {
  display: flex;
  justify-content: center;
  height: 100px;
  width: 100px;
}

.user_content3_projet_list_1_name {
  color: #0e3b5a;
  font-weight: bold;
  font-size: 1.2em;
}

.user_content3_projet_list_2_image {
  display: flex;
  justify-content: center;
  height: 100px;
  width: 100px;
}

.user_content3_projet_list_2_name {
  color: #0e3b5a;
  font-weight: bold;
  font-size: 1em;
}


.user_content3_projet_list_3_image {
  display: flex;
  justify-content: center;
  height: 100px;
  width: 100px;
  margin: 0;
}

.user_content3_projet_list_3_name {
  color: #0e3b5a;
  font-weight: bold;
  font-size: 1.2em;
}

.liste {
  text-align: left;
  overflow-y:scroll; 
  position:relative;
  height: 300px;
}
</style>