<template>
  <v-container fluid> </v-container>
</template>

<script lang="ts">
import { Component, Vue, Watch, Prop } from "vue-property-decorator";
import HelloWorld from "../components/HelloWorld.vue";
import Axios from "axios";

@Component
export default class Home extends Vue {}
</script>
