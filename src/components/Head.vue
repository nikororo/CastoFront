<template>
  <div>
    <header class="header_okr">
      <div class="soft_menu">
        <router-link href="" class="home_main" to="/">
          <img src="../style/img/Logo.png" alt="Logo" class="logo_okr icon_logo">
        </router-link>
      </div>
      <div class="user_menu">
        <img src="../style/img/Bell.png" alt="Bell" class="bell_okr icon_bell">
        <p class="use_name" v-if="this.$store.state.user">
          {{ this.$store.state.user.name }}
        </p>
        <img src="../style/img/User.png" alt="Photo" class="user_photo icon_user">

        <div class="menu">
          <a class="button_menu"><img src="../style/img/Menu.png" alt=""></a>
          <div class="links_menu">
            <div class="tre"></div>
            <div class="btnLogOut">
              <router-link to="/settingsUser">
                <img width="25" height="25" src="../style/img/Settings.png" alt="">
                <span>Настройки</span>
              </router-link>
            </div>
            <div>
              <button @click="showLogOutModal = true" class="btnLogOut">
                <img width="25" height="25" src="../style/img/Exit.png" alt="Log Out">
                <span>Выход</span>
              </button>
            </div>
          </div>
        </div>
        <LogOutModal v-if="showLogOutModal" @close="showLogOutModal = false"/>
      </div>
    </header>
  </div>
</template>

<script>
import LogOutModal from './LogOutModal';

export default {
  name: 'Head',

  components: {
    LogOutModal
  },

  data: () => ({
    showLogOutModal: false,
  })
}
</script>

<style scoped>
.menu {
  position: relative;
}

.btnLogOut a {
  text-decoration: none;
}

</style>