<template>
  <div id="app">
    <header>
      <h1>My iAndroid@Mp3</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">
          <div class="imageAlbum">
            <img :src="current.img" />
          </div>
          <span>Artist : {{current.artist}} </span> - <span>Title : {{current.title}} </span><br>
        </h2>
          <div class="pannel">
            <button class="prev" @click="previous">Prev</button>
            <button class="play" @click="play" v-if="!playing">Play</button>
            <button class="pause" @click="pause" v-else >Pause</button>
            <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3> Playlist </h3>
        <p v-for="song in songs" :key="song.title" @click="play(song)">{{song.artist}} - {{song.title}} </p>
        
      </section>
    </main>
  </div>
  
</template>




<script>
  export default {
    name:'app',

    data() {
      return{

        current: {},
        index:0,
        playing: false,

        songs: [
          {
            title:'Origami',
            artist:'Maitre Gims',
            src: require('./assets/gims-origami.mp3'),
            img: require('./assets/gimsAlbum.jpg')
          },

          {
            title:'Tout va bien',
            artist:'Maitre Gims',
            src: require('./assets/gims-tout-va-bien.mp3'),
            img: require('./assets/gimsAlbum.jpg')
          },

          {
            title:'SICARIO',
            artist:'Maitre Gims',
            src: require('./assets/gims-sicario.mp3'),
            img: require('./assets/gimsAlbum2.jpg')
          }


        ],

        player: new Audio() // Si tu call player tu va lancer l'audio

      }
    },

    methods: {

      play(song) {
        if(typeof song.src !="undefined") {
          this.current = song;
          
          this.player.src = this.current.src;
        }
        this.player.play();
        this.playing = true;
      },

      pause() {
        this.player.pause();
        this.playing = false;

      },

      next() {
        this.index++;
        if(this.index > this.songs.length - 1) {
          this.index = 0;
        }
        this.current = this.songs[this.index];
        this.play(this.current);

      },

      previous() {

        this.index++;
        if(this.index > this.songs.length - 1) {
          this.index = 0;
        }
        this.current = this.songs[this.index];
        this.play(this.current);

      }
     
    },

    
        mounted() {
              this.current = this.songs[this.index];
              this.player.src = this.current.src;
              this.player.play();
            }

  }
</script>




<style>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
}



.imageAlbum {
 
 height: 350px;
 width: 350px;
margin-left: 39%;
}


.imageAlbum img {
  width: 100%;
  
}

main {
text-align: center;
margin: 50px;
background-color: rgb(206, 206, 206);
padding: 30px;
border-radius: 20px;
border: rgb(6, 6, 66) solid 5px;
}

.playlist {
 
  margin: 20px;
}

.playlist h3 {
 
background-color: rgb(6, 6, 66);
width: 100%;
color: white;
padding: 7px;
border-radius: 50px;
}

header {
  display:flex ;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 15px;
  background-color: rgb(6, 6, 66);
  color: white;
}


.prev, .next {
  background-color: rgb(6, 6, 66);
  color: white;
  border: solid 2px black;
  border-radius: 10px;
  padding: 15px 40px;
  margin: 15px

}

.play, .pause {
  background-color: rgb(6, 6, 66);
  color: white;
  border: solid 2px black;
  border-radius: 10px;
  padding: 30px 40px;
  margin: 15px

}

button:hover {
  color: red;
  border: solid 2px red;
}

.playlist p {
  font-weight: bold;
  font-size: 30px;
  cursor: pointer;
}

.playlist p:hover {
  color: red;
}

</style>
