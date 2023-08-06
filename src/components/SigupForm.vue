<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: '',
            terms: false,
            tempSkill: '',
            skills: [],
            passwordErr: ''
        }
    },
    methods: {
        addSkill(e) {
            if (e.key === ',' && this.tempSkill) {
                if(!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill);
                }
                
                this.tempSkill=''
            }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter(item => skill !== item)
        },
        handleSubmit(){
            this.passwordErr = this.password.length > 5? '' : "Password must be atleast 6 characters long";
            if(!this.passwordErr){
                console.log('Email:', this.email);
                console.log('Password:', this.password);
                console.log('Role:', this.role);
                console.log('Skills:', this.skills);
                console.log('Terms:', this.terms);
            }
        }
    }
}

</script>

<template>
    <form @submit.prevent="handleSubmit"> 
        <label>Email: </label>
        <input type="email" required v-model="email" />

        <label>Password: </label>
        <input type="password" required v-model="password" />
        <div v-if="passwordErr" class="error">
            <span>{{ passwordErr }}</span>
        </div>

        <label>Role: </label>
        <select v-model="role">
            <option value="Front End Developer">Front End Developer</option>
            <option value="Back End Developer">Back End Developer</option>
            <option value="Full Stack Developer">Full Stack Developer</option>
        </select>

        <label>Skills</label>
        <input type="text" v-model="tempSkill" @keyup.alt="addSkill" />
        <div v-for="skill in skills" :key="skill" class="skill-sec" >
          <span @click="deleteSkill(skill)">{{ skill }}</span> 
        </div>

        <div class="terms">
            <input type="checkbox" v-model="terms" required />
            <label>Accept Terms and Conditions</label>
        </div>

        <div class="submit">
            <button type=" submit">
                Create an Account
            </button>
        </div>

    </form>
    <p class="note"><i>Note: "The Create Button logs all the inputs in the console"</i></p>
</template>



<style scoped>
form {
    max-width: 420px;
    margin: 20px auto;
    background: #C0C0C0;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label {
    color: black;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6rem;
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
    color: black;
}

input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.skill-sec{
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: white;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: black;
    cursor: pointer;
}
button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit {
    text-align: center;
}
.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
p.note{
    display: inline-block;
    justify-content: center;
    text-align: center;
    width: 420px;
    background: green;
    color: white;
}
</style>