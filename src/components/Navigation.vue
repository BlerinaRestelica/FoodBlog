<template>
  <header>
    <nav class="container">
      <div class="branding">
        <router-link class="header" :to="{ name: 'Home' }">
          Food Stories
        </router-link>
      </div>
      <div class="nav-links">
        <ul v-show="!mobile">
          <router-link class="link" :to="{name: 'Home'}"> Home </router-link>
          <router-link class="link" :to="{name: 'Blogs'}"> Blogs </router-link>
          <router-link class="link" to="#"> Create Post </router-link>
          <router-link class="link" to="#"> Login/Register </router-link>
        </ul>
      </div>
    </nav>
    <!-- this nav bar is needed for mobile app -->
    <menuIcon @click="toogleMobileNav" class="menu-icon" v-show="mobile" />
    <transition name="mobile-nav">
      <ul class="mobile-nav" v-show="mobileNav">
        <router-link class="link" :to="{name: 'Home'}"> Home </router-link>
        <router-link class="link" :to="{name: 'Blogs'}"> Blogs </router-link>
        <router-link class="link" to="#"> Create Post </router-link>
        <router-link class="link" to="#"> Login/Register </router-link>
      </ul>
    </transition>
  </header>
</template>

<script>
//import { component } from 'vue/types/umd';
import menuIcon from "../assets/Icons/bars-regular.svg";

export default {
  name: "navigation",
  components: {
    menuIcon,
  },
  data() {
    return {
      mobile: null,
      mobileNav: null,
      windownWidth: null,
    };
  },
  created() {
    window.addEventListener("resize", this.checkScreen);
    this.checkScreen();
  },
  //fnciton that checks the size of app
  methods: {
    checkScreen() {
      this.windownWidth = window.innerWidth;
      if (this.windownWidth <= 750) {
        this.mobile = true;
        return;
      }
      this.mobile = false;
      this.mobileNav = false;
      return;
    },

    toogleMobileNav() {
      this.mobileNav = !this.mobileNav;
    },
  },
};
</script>
<!--the scoped tag means that the styles we add in this component only stay within this component -->
<style lang="scss" scoped>
header {
  background-color:  rgba(53, 139, 53, 0.445);
  padding: 0 25px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.06);
  z-index: 99;
  .header {
    font-weight: 600;
    font-size: 24px;
    color: black;
    text-decoration: none;
    &:hover {
      color: rgba(3, 141, 33, 0.986);
    }
  }

  .link {
    font-weight: 500;
    padding: 0 8px;
    transition: 0.3s color ease;

    &:hover {
      color:  rgb(3, 141, 33);
    }
  }

  nav {
    display: flex;
    padding: 25px 0;

    .barnding {
      display: flex;
      align-items: center;
    }
    .nav-links {
      position: relative;
      display: flex;
      flex: 1;
      align-items: center;
      justify-content: flex-end;

      ul {
        margin-right: 32px;

        .link {
          margin-right: 32px;
        }
        .linl:last-child {
          margin-right: 0;
        }
      }
    }
  }

  .menu-icon {
    cursor: pointer;
    position: absolute;
    top: 32px;
    right: 25px;
    height: 25px;
    width: auto;
  }
  .mobile-nav {
    padding: 20px;
    width: 70%;
    max-width: 250px;
    display: flex;
    flex-direction: column;
    position: fixed;
    height: 100%;
    background-color: rgb(119, 118, 118);
    top: 0;
    left: 0;

    .link {
      padding: 15px;
      color: white;
    }
  }
  .mobile-nav-enter-active,
  .mobile-nav-leave-active {
    transition: all 1s ease;
  }
  .mobile-nav-enter {
    transform: translateX(-250px);
  }
  .mobile-nav-enter-to {
    transform: translateX(0);
  }
  .mobile-nav-leave-to {
    transform: translateX(-250px);
  }
}
</style>
