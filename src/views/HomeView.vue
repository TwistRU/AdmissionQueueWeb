<script setup lang="ts">
import { onMounted, reactive, watch } from 'vue';
import { useUser, useAuth } from 'vue-auth3';
const auth = useAuth();
const user = useUser();
const roles = reactive({ Operators: false, Registrators: false, Admins: false });
watch(
  user,
  () => {
    if (user.value?.groups) {
      user.value.groups.forEach((x: string) => {
        roles[x] = true;
      });
    } else {
      roles.Registrators = false;
      roles.Operators = false;
      roles.Admins = false;
    }
  },
  { immediate: true }
);
</script>
<template>
  <section class="hero is-large container">
    <div class="hero-body">
      <div class="columns">
        <b-button
          v-show="roles.Operators"
          tag="router-link"
          :to="{ name: 'operator_settings' }"
          class="column is-large is-primary"
        >
          Оператор
        </b-button>
        <div class="column is-0"></div>
        <b-button
          v-show="roles.Registrators"
          tag="router-link"
          :to="{ name: 'registrator' }"
          class="column is-large is-primary"
        >
          Ресепшен
        </b-button>
      </div>
    </div>
  </section>
</template>
