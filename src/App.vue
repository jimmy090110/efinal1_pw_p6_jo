<template>
  <div class="border">
    <div v-if="jugarOn">
      <div class="score">
        <p>puntaje:{{ puntaje }}</p>
        <p>intentos:{{ intentos }}</p>
      </div>
      <div class="comp1">
        <Pokemon :imagen="img1" :texto="texto1" />
        <Pokemon :imagen="img2" :texto="texto2" />
        <Pokemon :imagen="img3" :texto="texto3" />
      </div>
      <div class="boton">
        <button @click="jugar">JUGAR</button>
      </div>
    </div>
    <div v-else>
      <div v-if="intentos >= 5 && puntaje<=10" :style="{ color: 'red', textAlign: 'center' }">
        <p>Haz utilizado tus 5 intentos</p>
        <p>El juego ha terminado, intentalo nuevamente</p>
        <div class="boton">
          
          <button @click="newgame">Nuevo Juego</button>
        </div>
      </div>
      <div v-if="puntaje >= 10 && intentos<=5" :style="{ color: 'blue', textAlign: 'center' }">
        <p>Puntaje:{{ puntaje }}</p>

        <p>Felicidades has ganado un premio de $10.000,00</p>
        <div class="boton">
          <button @click="newgame">Nuevo Juego</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Pokemon from "./components/Pokemon.vue";

export default {
  name: "App",
  components: {
    Pokemon,
  },
  data() {
    return {
      img1: "https://via.placeholder.com/250",
      texto1: "xxxxxxx",
      img2: "https://via.placeholder.com/250",
      texto2: "xxxxxxx",
      img3: "https://via.placeholder.com/250",
      texto3: "xxxxxxx",
      puntaje: 0,
      intentos: 0,
      jugarOn: true,
    };
  },
  methods: {
    newgame() {
      this.img1 = "https://via.placeholder.com/250";
      this.texto1 = "xxxxxxx";
      this.img2 = "https://via.placeholder.com/250";
      this.texto2 = "xxxxxxx";
      this.img3 = "https://via.placeholder.com/250";
      this.texto3 = "xxxxxxx";
      this.puntaje = 0;
      this.intentos = 0;
      this.jugarOn = true;
    },

    async jugar() {
      this.intentos++;
      const id1 = Math.floor(Math.random() * 5) + 1;
      const data1 = await this.ObtenerName(id1);
      this.texto1 = data1.name;
      this.img1 =
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/" +
        id1 +
        ".svg";

      const id2 = Math.floor(Math.random() * 5) + 1;
      const data2 = await this.ObtenerName(id2);
      this.texto2 = data2.name;
      this.img2 =
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/" +
        id2 +
        ".svg";

      const id3 = Math.floor(Math.random() * 5) + 1;
      const data3 = await this.ObtenerName(id3);
      this.texto3 = data3.name;
      this.img3 =
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/" +
        id3 +
        ".svg";

      if (this.img1 == this.img2 && this.img2 == this.img3) {
        this.puntaje += 5;
      } else if (this.img1 == this.img2 || this.img2 == this.img3 || this.img1 == this.img3) {
        this.puntaje += 2;
      } else {
        this.puntaje += 0;
      }

      if (this.intentos >= 5 || this.puntaje >= 10) {
        this.jugarOn = false;
      }
    },

    async ObtenerName(id) {
      return await fetch("https://pokeapi.co/api/v2/pokemon/" + id).then((r) =>
        r.json()
      );
    },
  },
};
</script>

<style>
.border {
  border: 2px solid black;
  margin-left: 200px;
  margin-right: 200px;
}
.score {
  display: flex;
  flex-direction: row;
  justify-content: center;
  
}
p {
  margin: 20px;
  font-size: 20px;
}

.comp1 {
  display: flex;
  direction: row;
  justify-content: center;
}

button {
  border: solid black 3px;
  margin-bottom: 10px;
  width: 120px;
  height: 40px;
}

.boton {
  display: flex;
  justify-content: center;
}
</style>
