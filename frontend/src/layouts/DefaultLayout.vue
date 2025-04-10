<template>
  <header class="header">
    <!--   Шаблон   --->
    <div class="header__user">
      <!--   Шаблон   --->
      <div
        v-if="authStore.isAuthenticated"
        class="header__logout"
        @click="logout"
      >
        <span>Выйти</span>
      </div>
      <router-link v-else :to="{ name: 'login' }" class="header__logout">
        <span>Войти</span>
      </router-link>
    </div>
  </header>
</template>

<script setup>
import { useAuthStore } from "@/stores/auth";
import { useRouter } from "vue-router";
import { useCartStore } from "@/stores/cart";
import { getPublicImage } from "@/common/helpers/public-image";

const authStore = useAuthStore();
const cartStore = useCartStore();
const router = useRouter();

const logout = async () => {
  await authStore.logout();
  await router.replace({ name: "login" });
};
</script>
