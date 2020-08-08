<template>
  <div class="dashboard-container">
    <div class="dashboard-text">name: {{ name }}</div>
    <div class="first">
      <el-row>
        <router-link to="/lists/doctors">
          <el-button type="primary" plain> Listes des Medecins</el-button>
        </router-link>
        <router-link to="/lists/nurses">
          <el-button type="primary" plain>Listes des Infirmiers</el-button>
        </router-link>
      </el-row>
    </div>
    <div class="first">
      <router-link to="/lists/rdv_hosp">
        <el-button type="success" plain>
          Listes des Rdvs Hospitalisation</el-button
        >
      </router-link>
    </div>
    <div class="first">
      <router-link to="/lists/rdv_hj">
        <el-button type="success" plain>
          Listes des Rdvs Hopital de Jour</el-button
        >
      </router-link>
      <router-link to="/lists/rdv_had">
        <el-button type="success" plain>
          Listes des Rdvs Hospitalisation à Domicile</el-button
        >
      </router-link>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  name: "Dashboard",
  computed: {
    ...mapGetters(["name"])
  }
};
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 10px;
    padding: 10px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
    text-align: center;
  }
}
.first {
  padding: 10px;
  margin: 4px;
}
</style>
