<template>
  <form  @submit.prevent="handleSubmit">
    <label >Email</label>
    <input type="email" required v-model="email">

    <label >Password</label>
    <input type="password" required v-model="password">
    <div class="error" v-if="passwordError">
      {{passwordError}}
    </div>

    <label >Role:</label>
    <select v-model="role">
      <option selected value="developer">developer</option>
      <option value="designer">designer</option>
    </select>
    <label>Skills</label>
    
    <input type="text" v-model="tempSkill" @keyup="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill">
    <span @click="deleteSkill(skill)">{{skill}}</span>
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="terms">
      <label>Accept terms and condition</label> 
    </div>

    <div class="submit">
         <button>Create an Account</button>
    </div>
  </form>

  <p> EMAIL: {{email}}</p>
  <p>Password: {{password}}</p>
  <p>Role: {{role}}</p>
  <p>Terms: {{terms}}</p>
 
</template>

<script>
export default {
data(){
  return {
 email:'',
 password:'',
 role:'',
 terms:false,
 tempSkill:'',
 skills:[],
 passwordError:'',



  }
},
methods:{
  addSkill(e){
       if(e.key===',' && this.tempSkill)
       {
         if(!this.skills.includes(this.tempSkill)){
             
           this.skills.push(this.tempSkill)
         }
         this.tempSkill=''
       }
  },
  deleteSkill(skill)
  {
    this.skills=this.skills.filter((item)=>{
        return skill !==item
    })
  },
  handleSubmit()
  {
     this.passwordError=this.password.length > 5 ?'' :'password must be at least 6 chars long'
  }
}
}
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: #fff;
  text-align: left ;
  padding: 40px;
  border-radius: 10px;

}

label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 1.6rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;

}

input,select{
  display: block;
  padding: 10px 6px;
  width: 100%;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}

input:focus{
  outline-color: aqua;
}

input[type="checkbox"]
{
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}


.pill {
  display: inline-block;
  margin:  20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius:20px ;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}

button {
  background: #0BF;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: #fff;
  border-radius:20px ;
}

.submit{
  text-align: center;
}

.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 1rem;
  font-weight: bold;
}
</style>