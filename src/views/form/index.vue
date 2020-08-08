<template>
  <div class="app-container">
    <el-form
      :model="ruleForm"
      :rules="rules"
      ref="ruleForm"
      label-width="120px"
      class="demo-ruleForm"
    >
      <el-form-item label="Type" prop="type">
        <el-select v-model="ruleForm.type" placeholder="Choisissez un Type">
          <el-option label="Medecin" value="Medecin"></el-option>
          <el-option label="Infirmier" value="Infirmier"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="Nom" prop="nom">
        <el-input v-model="ruleForm.nom"></el-input>
      </el-form-item>
      <el-form-item label="Prenom" prop="prenom">
        <el-input v-model="ruleForm.prenom"></el-input>
      </el-form-item>
      <el-form-item label="Grade" prop="grade">
        <el-input v-model="ruleForm.grade"></el-input>
      </el-form-item>
      <el-form-item label="Username" prop="username">
        <el-input v-model="ruleForm.username"></el-input>
      </el-form-item>
      <el-form-item label="Password" prop="password">
        <el-input
          type="password"
          v-model="ruleForm.password"
          autocomplete="off"
        ></el-input>
      </el-form-item>
      <el-form-item label="Confirm" prop="checkPass">
        <el-input
          type="password"
          v-model="ruleForm.checkPass"
          autocomplete="off"
        ></el-input>
      </el-form-item>
      <el-form-item label="Mobile" prop="mobile">
        <el-input
          type="mobile"
          v-model.number="ruleForm.mobile"
          autocomplete="off"
        ></el-input>
      </el-form-item>
      <el-form-item label="Email" prop="email">
        <el-input v-model="ruleForm.email"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')"
          >Créer</el-button
        >
        <el-button @click="resetForm('ruleForm')">Réinitialiser</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  data() {
    var validatePass = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("Veuillez entrer le mot de passe"));
      } else {
        if (this.ruleForm.checkPass !== "") {
          this.$refs.ruleForm.validateField("checkPass");
        }
        callback();
      }
    };
    var validatePass2 = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("Veuillez entrer à nouveau le mot de passe"));
      } else if (value !== this.ruleForm.password) {
        callback(new Error("Les deux entrées ne correspondent pas!"));
      } else {
        callback();
      }
    };
    return {
      ruleForm: {
        type: "",
        nom: "",
        prenom: "",
        grade: "",
        username: "",
        password: "",
        checkPass: "",
        mobile: "",
        email: ""
      },
      rules: {
        type: [
          {
            required: true,
            message: "Veuillez entrer votre Type",
            trigger: "change"
          }
        ],
        nom: [
          {
            required: true,
            message: "Veuillez entrer votre Nom",
            trigger: "blur"
          }
        ],
        prenom: [
          {
            required: true,
            message: "Veuillez entrer votre Prenom",
            trigger: "blur"
          }
        ],
        grade: [
          {
            required: true,
            message: "Veuillez entrer votre Grade",
            trigger: "blur"
          }
        ],
        username: [
          {
            required: true,
            message: "Veuillez entrer votre Username",
            trigger: "blur"
          }
        ],
        password: [
          { validator: validatePass, trigger: "blur", required: true }
        ],
        checkPass: [
          { validator: validatePass2, trigger: "blur", required: true }
        ],
        mobile: [
          { required: true, message: "Veuillez entrer le Numéro" },
          { type: "number", message: "le numéro doit être un nombre" }
        ],
        email: [
          {
            required: true,
            message: "Veuillez entrer votre Email",
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
</style>
