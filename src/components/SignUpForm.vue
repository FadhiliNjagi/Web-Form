<template>
    <form action="" @submit.prevent="handleSubmit">
        <label for="email">Email:</label>
        <input type="email" v-model="email" required>
        <label for="password">Password:</label>
        <input type="password" v-model="password" required>
        <p v-if="passwordError" class="error">{{ passwordError }}</p>

        <label for="role">Role:</label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <label for="expertise">Expertise</label>
        <div>
            <input type="checkbox" value="frontend" v-model="expertise">
            <label for="expertise">Front End</label>
        </div>
        <div>
            <input type="checkbox" value="backend" v-model="expertise">
            <label for="expertise">Back End</label>
        </div>
        <div>
            <input type="checkbox" value="devops" v-model="expertise">
            <label for="expertise">Dev Ops</label>
        </div>

        <label for="skills">Skills:</label>
        <input type="text" v-model="tempSkill" @keyup="addSkill">
        <div v-for="skill in skills" :key="skill" class="skill">
            <p>{{ skill }}<span @click="removeSkill(skill)" class="x-btn">&#10006;</span></p>
        </div>

        <div class="terms">
            <input type="checkbox" name="terms" id="terms" v-model="acceptedTerms">
            <label for="terms">Accept terms and conditions</label>
        </div>

        <div class="submit">
            <button>Create Account</button>
        </div>
    </form>

    <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>Terms accepted: {{ acceptedTerms }}</p>
    <p>Expertise: {{ expertise }}</p>
    <p>Skills: {{ skills }}</p>
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: 'designer',
            acceptedTerms: false,
            expertise: [],
            tempSkill: '',
            skills: [],
            passwordError: ''
        }
    },
    methods: {
        addSkill(e) {
            if (e.key == "," && this.tempSkill) {
                this.tempSkill = this.tempSkill.slice(0, -1)
                this.tempSkill = this.tempSkill.trim()
                if (!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill.trim())
                }
                this.tempSkill = ''
            }
        },
        removeSkill(skill) {
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit() {
            // validate password
            this.passwordError = this.password.length > 5 ?
             "" : 'Password must be at least 6 characters long'
        }
    },
}
</script>

<style>
form {
    max-width: 420px;
    margin: 10px auto;
    background: white;
    text-align: left;
    padding: 20px 40px;
    border-radius: 10px;
}
label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.7em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select {
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
.skill {
    display: inline-block;
    margin: 10px 10px 0 0;
    padding: 0px 10px;
    background: #eee;
    border-radius: 18px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
.x-btn {
    margin-left: 5px;
    color: #555;
}
button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    font-size: medium;
}
.submit {
    text-align: center;
}
.error {
    color: red;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>