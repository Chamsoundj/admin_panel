<template>
  <div class="app-container">
    <div class="top">
      <el-row>
        <router-link to="/lists/consultation">
          <el-button type="primary" plain>
            Voir la liste des Consultation</el-button
          >
        </router-link>
      </el-row>
    </div>
    <div>
      <el-form
        :model="ruleForm"
        :rules="rules"
        ref="ruleForm"
        label-width="110px"
        class="demo-ruleForm"
      >
        <el-form-item label="Nom" prop="firstname">
          <el-input v-model="ruleForm.firstname"></el-input>
        </el-form-item>
        <el-form-item label="Prenom" prop="lastname">
          <el-input v-model="ruleForm.lastname"></el-input>
        </el-form-item>
        <el-form-item label="Date de Naissance" prop="birthdate">
          <el-col :span="11">
            <el-date-picker
              type="date"
              placeholder="Choisissez une date"
              v-model="ruleForm.birthdate"
              style="width: 100%;"
            ></el-date-picker>
          </el-col>
        </el-form-item>
        <el-form-item
          label="Age"
          prop="age"
          :rules="[
            { required: true, message: 'Veuillez entrer l\'âge' },
            { type: 'number', message: 'l\'âge doit être un nombre' }
          ]"
        >
          <el-input
            type="age"
            v-model.number="ruleForm.age"
            autocomplete="off"
          ></el-input>
        </el-form-item>
        <el-form-item label="Motif" prop="motif">
          <el-input type="textarea" v-model="ruleForm.motif"></el-input>
        </el-form-item>
        <el-form-item label="Diagnostic" prop="diagnostic">
          <el-input type="textarea" v-model="ruleForm.diagnostic"></el-input>
        </el-form-item>
        <el-form-item label="Décision du Medecin" prop="decision">
          <el-select
            v-model="ruleForm.decision"
            placeholder="Décision du Medecin"
          >
            <el-option label="Consultation" value="Consultation"></el-option>
            <el-option
              label="Hospitalisation"
              value="Hospitalisation"
            ></el-option>
            <el-option
              label="Hopital de Jour"
              value="Hopital de Jour"
            ></el-option>
            <el-option
              label="Hospitalisation à Domicile"
              value="Hospitalisation à Domicile"
            ></el-option>
          </el-select>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm('ruleForm')"
            >Créer</el-button
          >
          <el-button @click="resetForm('ruleForm')">Réinitialiser</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      ruleForm: {
        firstname: "",
        lastname: "",
        birtdate: "",
        age: "",
        motif: "",
        diagnostic: "",
        decision: ""
      },
      rules: {
        firstname: [
          {
            required: true,
            message: "Veuillez entrer le Nom",
            trigger: "blur"
          }
        ],
        lastname: [
          {
            required: true,
            message: "Veuillez entrer le Prenom",
            trigger: "blur"
          }
        ],
        decision: [
          {
            required: true,
            message: "Veuillez coisissez une Décision",
            trigger: "change"
          }
        ],
        birthdate: [
          {
            type: "date",
            required: true,
            message: "Veuillez entrer la Date",
            trigger: "change"
          }
        ],
        motif: [
          {
            required: true,
            message: "Veuillez entrer le Motif",
            trigger: "blur"
          }
        ],
        diagnostic: [
          {
            required: true,
            message: "Veuillez entrer le Diagostic",
            trigger: "blur"
          }
        ]
      }
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  }
};
</script>

<style scoped>
.line {
  text-align: center;
}
.top {
  text-align: right;
  margin: 4px;
  }
</style>
