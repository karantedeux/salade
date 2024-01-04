<template>
  <section id="add">
    <img id="juno" src="./assets/JunoinParis.png">
    <div id="add__block">
      <span>+</span>
      <form @submit.prevent="addPlayer">
        <label>Nom du joueur :</label>
        <input v-model="newPlayer.nom" required>
        <label>Gardien:</label>
        <input type="checkbox" v-model="newPlayer.isGoalie">
        <button type="submit">Ajouter</button>
      </form>
    </div>
    <img id="logotype" src="./assets/OSFsansfond.png">
  </section>

  <section id="list">
    <div id="list__title">
      <h2>Liste des participants</h2>
      <div title="3, 6, 9, 12, 15, 18, 21, 24, 27, 30, 33, 36, 39, 42, 45, 48, 51 ,54 , 57, 60" id="list__count" v-data="joueurs">
        <span>{{ joueurs.length }}<p>PARTICIPANTS</p></span>
      </div>
      <div id="list__count__goalie">
        <span>{{ joueurs.filter(joueur => joueur.isGoalie).length }}</span>
        <p>Gardiens</p>
      </div>
      <div id="list__count__forward">
        <span>{{ joueurs.filter(joueur => !joueur.isGoalie).length }}</span>
        <p>Attaquants</p>
      </div>
    </div>

    <ul>
      <li v-for="joueur in joueurs" :key="joueur.id">
        <p>{{ joueur.nom }}</p> <span>{{ joueur.isGoalie ? 'Gardien' : 'attaquant' }}</span>
        <button @click="supprimerJoueur(joueur)">Supprimer</button>
      </li>
    </ul>
  </section>

  <div id="teamgen">
    <button @click="teamGen">Génerer les équipes</button>
  </div>

  <section id="teams">
    <h2>Liste des équipes</h2>
    <div id="teams__block">
      <ul>
        <li class="zoomIn" id="teams__block__items" v-for="(equipe, index) in equipes" :key="index">
          <h3 :style="{ backgroundColor: colors[index % colors.length] }">Équipe {{ index + 1 }}</h3>
          <div id="teams__block__items__players" v-for="joueur in equipe" :key="joueur.id">
            <p>{{ joueur.nom }}</p>
            <span>{{ joueur.isGoalie ? 'Gardien' : 'attaquant' }}</span>
          </div>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      newPlayer: {
        nom: '',
        isGoalie: false
      },
      nombreParticipants: 0,
      joueurs: [],
      equipes: [],
      colors: [
        '#4a006f',
        '#470a77',
        '#45147e',
        '#421e86',
        '#3f288d',
        '#3d3195',
        '#3a3b9c',
        '#3745a4',
        '#354fab',
        '#3259b3',
        '#941b85',
        '#871c84',
        '#7b1e83',
        '#6e1f82',
        '#612081',
        '#552280',
        '#48237f',
        '#3b247e',
        '#2f267d',
        '#22277c'
      ]
    };
  },
  methods: {
    addPlayer() {
      this.joueurs.push({ ...this.newPlayer });
      this.newPlayer.nom = '';
      this.newPlayer.isGoalie = false;
      this.nombreParticipants = this.joueurs.length;
    },
    supprimerJoueur(joueur) {
      const index = this.joueurs.indexOf(joueur);
      if (index !== -1) {
        this.joueurs.splice(index, 1);
        this.nombreParticipants = this.joueurs.length;
      }
    },
    teamGen() {
      const nombreEquipes = Math.floor(this.nombreParticipants / 3);
      this.equipes = [];

      const gardiens = this.joueurs.filter(joueur => joueur.isGoalie);
      const forwards = this.joueurs.filter(joueur => !joueur.isGoalie);
      forwards.sort(() => Math.random() - 0.5);

      let equipeIndex = 0;
      while (forwards.length > 0) {
        if (!this.equipes[equipeIndex]) {
          this.equipes[equipeIndex] = [];
        }

        const joueur = forwards.pop();
        this.equipes[equipeIndex].push(joueur);
        equipeIndex = (equipeIndex + 1) % nombreEquipes;
      }

      this.equipes.forEach(equipe => {
        const gardien = gardiens.pop();
        if (gardien) {
          equipe.push(gardien);
        }
      });
    }
  }
};
</script>

<style lang="scss">
.zoomIn {
  animation-name: zoomIn;
  animation-duration: 1s;
  animation-delay: 2s;
  animation-fill-mode: both;
  &:nth-child(2) {
    animation-delay: 4s;
    transition-delay: 0.2s;
  }
  &:nth-child(3) {
    animation-delay: 6s;
  }
  &:nth-child(4) {
    animation-delay: 8s;
  }
  &:nth-child(5) {
    animation-delay: 10s;
  }
  &:nth-child(6) {
    animation-delay: 12s;
  }
  &:nth-child(7) {
    animation-delay: 14s;
  }
  &:nth-child(8) {
    animation-delay: 16s;
  }
  &:nth-child(9) {
    animation-delay: 18s;
  }
  &:nth-child(10) {
    animation-delay: 20s;
  }
  &:nth-child(11) {
    animation-delay: 22s;
  }
  &:nth-child(12) {
    animation-delay: 24s;
  }
  &:nth-child(13) {
    animation-delay: 26s;
  }
  &:nth-child(14) {
    animation-delay: 28s;
  }
  &:nth-child(15) {
    animation-delay: 30s;
  }
  &:nth-child(16) {
    animation-delay: 32s;
  }
  &:nth-child(17) {
    animation-delay: 34s;
  }
  &:nth-child(18) {
    animation-delay: 36s;
  }
  &:nth-child(19) {
    animation-delay: 38s;
  }
  &:nth-child(20) {
    animation-delay: 40s;
  }
}

@-webkit-keyframes zoomIn {
  0% {
    opacity: 0;
    transform: scale3d(.3, .3, .3);
  }

  50% {
    opacity: 1;
  }
}

@keyframes zoomIn {
  0% {
    opacity: 0;
    transform: scale3d(.3, .3, .3);
  }

  50% {
    opacity: 1;
  }
}


* {
  margin: 0;
  padding: 0;
  font-family: 'Poppins', sans-serif;
  color: $white;
}

::-webkit-scrollbar {
  width: 5px;
  background-color: #6248b2;
}


::-webkit-scrollbar-track {
  background: $blue1;
}

::-webkit-scrollbar-thumb {
  background: #6248b2;
}


body {
  background-color: $blue0;
}

#juno {
  width: 150px;
  height: 150px;
  border-radius: 10px;
}

#logotype {
  width: 400px;
}

#add {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 2%;
  box-shadow: inset 0px -110px 38px -30px rgba(23, 42, 95, 1);
  row-gap: 30px;
  justify-content: space-between;
  background-image: url("./assets/lobby.png");
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;

  &__block {
    display: flex;
    align-items: center;
    column-gap: 10px;
    color: $white;
    padding: 0px 10px 0px 0px;
    width: max-content;
    background-color: $blue1;
    border-radius: 10px;
    border: 3px solid #6248b2;

    & span {
      background-color: $blue2;
      font-size: 50px;
      height: 100%;
      border-radius: 8px 0px 0px 8px;
    }

    & form {
      display: flex;
      align-items: center;
      column-gap: 15px;
    }

    & input {
      background-color: $blue2;
      border: none;
      padding: 5px;
      border-radius: 10px;
    }

    & button {
      background-color: $blue2;
      padding: 5px;
      cursor: pointer;
      border-radius: 10px;
      border: 2px solid #6248b2;
    }
  }
}

#teamgen {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: $blue2;
  box-shadow: inset 0px -100px 38px -10px $blue0;
  height: 150px;

  & button {
    background-color: $blue0;
    border: 2px solid #6047AF;
    font-family: 'Rubik Mono One', sans-serif;
    font-size: 20px;
    padding: 10px 20px;
    border-radius: 10px;
    transition: 0.6s;
    cursor: pointer;

    &:hover {
      background-color: #6047AF;
    }
  }
}

#list {
  display: flex;
  background-color: $blue2;
  height: 100%;
  padding: 1%;
  column-gap: 10px;

  &__title {
    background-color: $blue1;
    height: fit-content;
    & h2 {
      font-size: 15px;
      padding: 10px;
    }
  }

  &__count {
    display: flex;
    justify-content: center;
    align-items: center;
    background-image: url("./assets/juliette.gif");
    background-size: cover;
    height: 300px;

    & span {
      display: flex;
      justify-content: center;
      padding: 10px;
      font-family: 'Rubik Mono One', sans-serif;
      border-radius: 10px;
      font-size: 35px;
      align-items: center;
      flex-direction: column;
      background-color: #C8213A;

      & p {
        font-size: 14px;
      }
    }
    &__goalie {
      display: flex;
      align-items: center;
      & span {
        background-color: #6047AF;
        text-align: center;
        width: 30px;
        padding-left: 5px;
        padding-right: 5px;
      }
      & p {
        font-size: 14px;
        padding-left: 5px;
      }
    }
    &__forward {
      display: flex;
      align-items: center;
      & span {
        background-color: #6047AF;
        padding-left: 5px;
        text-align: center;
        width: 30px;
        padding-right: 5px;
      }
      & p {
        font-size: 14px;
        padding-left: 5px;
      }
    }
  }

  & ul {
    display: flex;
    flex-wrap: wrap;
    row-gap: 10px;
    width: 90%;
    column-gap: 10px;
    height: fit-content;

    & li {
      display: flex;
      justify-content: space-around;
      align-items: center;
      background-color: $blue1;
      column-gap: 5px;
      flex: 1 0 21%;
      width: 21%;
      border: 2px solid #6047AF;
      border-radius: 5px;
      height: fit-content;

      & p {
        font-size: 13px;
        font-family: 'Rubik Mono One', sans-serif;
      }

      & span {
        font-size: 11px;
        padding: 5px 8px;
        transform: skew(-5deg);
        background-color: $blue2;
        height: 100%;
      }

      & button {
        background: none;
        border: none;
        cursor: pointer;
        font-size: 10px;
        color: #C8213A;
      }
    }
  }
}

#teams {
  display: flex;
  flex-direction: column;
  height: fit-content;
  margin-bottom: 10%;

  & h2 {
    background-color: $blue2;
    border: 2px solid #6047AF;
    text-transform: uppercase;
    width: 20%;
    transform: skew(-10deg);
    padding-left: 10px;
    margin-left: 1%;
    margin-bottom: 2%;
  }

  &__block {
    display: flex;

    & ul {
      display: flex;
      flex-wrap: wrap;
      width: 100%;
      padding: 10px;
      justify-content: center;
      align-items: center;
      column-gap: 20px;
      row-gap: 20px;
    }

    &__items {
      display: flex;
      flex-direction: column;
      align-items: center;
      border-radius: 10px;
      row-gap: 5px;
      width: 100px;
      flex: 1 0 21%;
      list-style: none;
      height: 180px;
      background-color: $blue2;

      & h3 {
        text-transform: uppercase;
        width: 100%;
        font-size: 25px;
        padding-top: 5px;
        padding-bottom: 5px;
        text-align: center;
        border-radius: 8px 8px 0px 0px;
      }

      &__players {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100%;
        column-gap: 10px;

        & p {
          font-family: 'Rubik Mono One', sans-serif;
          font-size: 20px;
        }

        & span {
          background-color: $blue1;
          padding: 5px 10px;
          font-size: 11px;
          transform: skew(-10deg);
        }
      }
    }
  }
}</style>