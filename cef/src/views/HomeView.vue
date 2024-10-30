<template>
  <div class="home">
    <playerlistw msg="Welcome to Your Vue.js App"/>
    <player_itemw msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import player_itemw from '@/components/PlayersList/playerItem.vue'
import playerlistw from '@/components/PlayersList/playerList.vue'

export default {
  name: 'HomeView',
  components: {
    playerlistw,
    player_itemw
  }
}
</script>
