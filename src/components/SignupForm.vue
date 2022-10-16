<template>
  <form>
    <label>Email</label>
    <input type="email" required v-model="email" />

    <label>Password</label>
    <input type="password" required v-model="password" />

    <label>Role:</label>
    <select v-model="role">
        <option value="Developer">Developer</option>
        <option value="Web Designer">Web Desginer</option>
    </select>

    <label>Skills</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill" />
    <div v-for="skill in skills" :key="skill" class="pill">
        {{skill}}
    </div>

    <div class="terms">
        <input type="checkbox" required v-model="terms" />
        <label>Accept terms and conditions</label>
    </div>


    
</form>
  <p>Email: {{email}} -- Password: {{password}}</p>
  <p>Password: {{password}}</p>
  <p>Role: {{role}}</p>
  <p>Terms: {{terms}}</p>
  <p>Names: {{names}}</p>
</template>

<script>
export default {
    data(){
        return{
            email: null,
            password: null,
            role: "Web Designer",
            terms: false,
            names: [],
            tempSkill: "",
            skills: []
        }
    },
    methods: {
        addSkill(event){
            if(event.keyCode === 188 && this.tempSkill){
                const splitSkill = this.tempSkill.split(",")[0]
                if(!this.skills.includes(splitSkill)){
                    this.skills.push(splitSkill)
                }
                this.tempSkill = ""
            }
        }
    }
}
</script>

<style>
    form{
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label{
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: .6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input, select{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555; 
    }
    input[type="checkbox"]{
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }
    .pill{
        padding: 10px;
        letter-spacing: 1.5px;
        border-radius: 10px;
        border: 1px solid #ddd;
    }
</style>