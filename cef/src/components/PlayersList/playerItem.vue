<template>
  <li>
    <span>{{ player.name }} | Лвл админки: {{ player.adminlvl }} | ID: {{ player.id }} - {{ player.status }} </span>
    <div class="playerlist_main_buttons">
      <button @click="$emit('player_kick')">кик</button>
      <button @click="$emit('player_ban')">бан</button>
    </div>
  </li>
</template>

<script>
export default {
  props: {
    player: Object
  }
};
</script>

<style>
    li{
      background: rgba(52, 59, 71, 25%);
      border-radius: 1.1vh;

      height: 4.80225988700565vh;
      width: 60vh;

      display: flex;
      align-items: center;

      box-sizing: border-box;
      padding-left: 2vh;

      font-size: 1.5vh;
    }
    button{
      background: rgba(7, 8, 8, 0.521);
      border-radius: .7vh;

      color: white;

      border:none;
      outline: none;

      font-size: 1.35vh;
    }
    .playerlist_main_buttons{
      display: flex;
      align-items: center;

      gap:1vh;
    }
</style>