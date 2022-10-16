<template>
  <form @submit.prevent="handleSubmit">
    <label>Email</label>
    <input type="email" required v-model="email" />

    <label>Password</label>
    <input type="password" required v-model="password" />
    <div v-if="passwordInvalid" class="invalidPassword">
      {{ passwordInvalid }}
    </div>

    <label>Role:</label>
    <select v-model="role">
      <option value="Developer">Developer</option>
      <option value="Web Designer">Web Desginer</option>
    </select>

    <label>Skills</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill" />
    <div
      v-for="skill in skills"
      :key="skill"
      class="pill"
      @click="removeSkill(skill)"
    >
      {{ skill }}
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="terms" />
      <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>Create Account</button>
    </div>
  </form>
  <p>Email: {{ email }} -- Password: {{ password }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms: {{ terms }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: null,
      password: null,
      role: "Web Designer",
      terms: false,
      names: [],
      tempSkill: "",
      skills: [],
      passwordInvalid: "",
      user: {
        email: this.email,
        password: this.password,
        roles: this.role,
        terms: this.terms,
        skills: this.skills
      },
    };
  },
  methods: {
    addSkill(event) {
      if (event.keyCode === 188 && this.tempSkill) {
        const splitSkill = this.tempSkill.split(",")[0];
        if (!this.skills.includes(splitSkill)) {
          this.skills.push(splitSkill);
        }
        this.tempSkill = "";
      }
    },
    removeSkill(skillToRemove) {
      this.skills = this.skills.filter((skill) => skill !== skillToRemove);
    },
    handleSubmit() {
      this.passwordInvalid = this.password.length >= 8 ? "" : "Password must be at least 8 characters long";
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1.25px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
button {
  width: 100%;
  background: #0b6dff;
  border: 0;
  padding: 15px 0px;
  margin-top: 20px;
  color: white;
  border-radius: 10px;
  cursor: pointer;
  font-weight: bold;
  letter-spacing: 0.25px;
  font-size: 1rem;
}
button:hover {
  background: #3a89ff;
  transition: 0.45s ease;
}
.submit {
  width: 100%;
  text-align: center;
}
.invalidPassword {
  margin: 5px 0 0 0;
  color: red;
  font-size: 12px;
}
</style>
