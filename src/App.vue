<template>
  <div id="system_main_container">
    <Loading v-show="globalVariables.statusDataLoaded == 0" />
    <template v-if="statusSiteLoaded==1">
      <ThemeLogged/>
    </template>
  </div>
</template>
<script setup>
  import globalVariables from "@/assets/globalVariables";
  import systemFunctions from "@/assets/systemFunctions";
  import toastFunctions from "@/assets/toastFunctions";

  import ThemeLogin from "@/components/themes/ThemeLogin.vue";
  import ThemeLogged from "@/components/themes/ThemeLogged/Index.vue";
  import Loading from "@/components/busy-states/Loading.vue";

  import {ref } from 'vue';
  import axios from 'axios';

  import {useRoute,useRouter} from 'vue-router';
  const route =useRoute()
  const router =useRouter()

  //global axios end
  let statusSiteLoaded=ref(1);
</script>