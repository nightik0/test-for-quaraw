<template>
  <div class="playerlist">
    <h1>Список игроков</h1>
    <input v-model="filter" placeholder="Фильтер" />
    <div class="playerlist_main">
      <ul>
        <player_itemw 
          v-for="player in filteredPlayers" 
          :key="player.id" 
          :player="player" 
          @player_kick="player_kick(player.id)" 
          @player_ban="player_ban(player.id)"
        />
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import player_itemw from './playerItem.vue';
import './fonts/stylesheet.css';

export default {
  components: { 
    player_itemw
  },
  data() {
    return {
      players: [
        { id: 1, name: 'Night', adminlvl: 10, status: 'Онлайн' },
        { id: 2, name: 'Quaraw',  adminlvl: 10, status: 'Онлайн' },
        { id: 2, name: 'Quaraw',  adminlvl: 10, status: 'Офлайн' },
        { id: 2, name: 'Quaraw',  adminlvl: 10, status: 'Офлайн' },
        { id: 2, name: 'Quaraw',  adminlvl: 10, status: 'Онлайн' },
        { id: 3, name: 'Merumond',  adminlvl: 52, status: 'Онлайн' },
        { id: 4, name: 'Kycher',  adminlvl: 4, status: 'Забанен' }
      ],
      filter: ''
    };
  },
  computed: {
    filteredPlayers() {
      return this.players.filter(player => 
        player.status.toLowerCase().includes(this.filter.toLowerCase())
      );
    }
  },
  mounted() {
    this.fetchPlayers();
  },
  methods: {
    async fetchPlayers() {
      try {
        const response = await axios.get('/api/players');
        this.players = response.data;
      } catch (error) {
        console.error(`Ошибка, кирил пукнул!`, error);
      }
    },
    async player_kick(playerId) {
      if (confirm(`Вы уверены, что хотите кикнуть игрока с ID ${playerId}?`)) {
        await axios.post('/api/kick', { id: playerId });
        this.fetchPlayers();
      }
    },
    async player_ban(playerId) {
      if (confirm(`Вы уверены, что хотите забанить игрока с ID ${playerId}?`)) {
        await axios.post('/api/ban', { id: playerId });
        this.fetchPlayers();
      }
    }
  }
};
</script>

<style>
    .playerlist{
      position: absolute;
      top:50%;
      left:50%;
      transform: translate(-50%, -50%);

      display: flex;
      flex-direction: column;

      font-family: Acrom;

      color: white;

      background: #101013;
      border-radius: 1.7890772128060264vh;

      width: 67.41337099811676vh;
      height: fit-content;

      padding-bottom: 2.3vh;

      h1{
        text-align: center;

        font-size: 3vh;
      }

      ul{
        display: flex;
        flex-direction: column;

        gap:1vh;
      }
    }
    .playerlist_main{
      overflow-y: scroll;
        overflow-x: hidden;

        height: 30vh;
    }
    .playerlist_main::-webkit-scrollbar{
      display: none;
    }
    .playerlist input{
      background: #252525;
      border-radius: 1.1vh;

      font-size: 1.3vh;

      height: 2.80225988700565vh;
      width: 60vh;

      margin: 0 0 0 3.5vh;
      box-sizing: border-box;
      padding: 0 0 0 1.5vh;

      outline: none;
      border: none;

      color:white
    }
    .playerlist input::placeholder{
      font-size: 1.3vh;
    }
</style>