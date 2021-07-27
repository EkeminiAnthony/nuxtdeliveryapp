<template>
    <div class="container-fluid ">
        <Navbar />
        <div class="container margin_top">
            <div class="card shadow" >
            <div class="card-body">
                <form @submit.prevent="signup">
                    <h5 class="modal-title" id="exampleModalLabel">SIGN UP</h5>
                    <p>Please fill in this form to create an account!</p>
                    <hr>
                     
                    <div class="mt-3">
                         <label for="exampleInputEmail1 mt-5">Email Address</label>
                    <input type="text" class="form-control" placeholder="Email Address" v-model="auth.email">
                    </div>
                   
                    <div class="form-row mt-3">
                        <div class="col">
                        <label for="inputPassword5">Password</label>
                        <input type="password" id="inputPassword5" class="form-control" aria-describedby="passwordHelpBlock" v-model="auth.password">
                        <!-- <small id="passwordHelpBlock" class="form-text text-muted">
                        Your password must be 8-20 characters long, contain letters and numbers
                        </small> -->
                        </div>
                        
                    </div>
                    <div class="mt-3">
                        <button type="submit" class="btn btn-primary">
                            <span v-if="notloading">SIGN UP</span>
                            <div v-else><loader/></div>
                        </button>
                    </div>
                 
                 </form>
            </div>
            </div>
        </div>
    </div>
</template>

<script>
import firebase from 'firebase'
import Navbar from "@/components/Navbar.vue"
import loader from "@/components/loader.vue"
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
export default {
    components:{
        firebase, Navbar, ElementUI,loader
    },
    data(){
        return{
          auth:{
            email:'',
            password:''
          },
          notloading:true,
            
        }
    },
    created(){
         
      
        
    },
    methods: {
        
        signup(){
            this.notloading = false;
            firebase.auth().createUserWithEmailAndPassword(this.auth.email, this.auth.password)
                .then((userCredential) => {
                    // Signed in
                    var user = userCredential.user;
                    this.$message({
                        message: 'Signup successful!',
                        type: 'success'
                        });
                        this.notloading = true;
                    console.log(user)
                    this.$router.push('/delivery');
                    // ...
                })
                .catch((error) => {
                    var errorCode = error.code;
                    var errorMessage = error.message;
                    console.log(errorCode)
                    alert(errorMessage)
                    this.notloading = true;
                });
        }
        
        

    }
    
}

</script>

<style scoped>
.card{
    width: 50%;
    margin-left: 15rem;
    margin-bottom: 7rem;
}
.margin_top{
    margin-top: 13rem !important;
}
.click_pass{
    cursor: pointer;
}
.btn-primary {
    color: white;
    border-color: #f15f22 !important;
    background-color:  #f15f22 !important;
    text-transform: capitalize;
}
@media only screen and (max-width: 600px) {
.card{
    width: 100%;
    margin-left: 0;
}
.margin_top{
    margin-top: 13rem !important;
}
.click_pass{
    cursor: pointer;
} 
.form-row{
    display: block !important;
}
.form-row .col{
    margin-top : 1rem;
}
}
@media only screen and (min-width: 700px)  and (max-width: 1200px) {
.card{
    width: 70%;
    margin-left: 7rem !important;
}
.margin_top{
    margin-top: 5rem !important;
}
.click_pass{
    cursor: pointer;
} 
.form-row{
    display: block !important;
}
.form-row .col{
    margin-top : 1rem;
}
} 


</style>