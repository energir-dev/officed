<script>
import MicrosoftSvg from '../assets/microsoft.svg';
import SignUpFooter from './SignUpFooter.svelte';
import { push } from "svelte-spa-router";

let email = "";
</script>

<div class="wrapper">

<div class="container">

<div class="card">

<img src={MicrosoftSvg} alt="microsoft" class="logo"/>

<h2>Create your Microsoft account</h2>

<p class="subtitle">Enter your email address</p>

<div class="input-group">
<label>New email</label>

<div class="email-row">
<input type="email" bind:value={email}/>
<select>
<option>@outlook.com</option>
<option>@hotmail.com</option>
</select>
</div>

</div>

<div class="button-row">
<button class="next">Next</button>
</div>

<p class="signin">
Already have an account?
<a on:click={() => push('/login')}>Sign in</a>
</p>

</div>

</div>

<SignUpFooter/>

</div>


<style>

/* MOBILE FIRST */

.wrapper{
min-height:100vh;
background:white;
display:flex;
flex-direction:column;
justify-content:space-between;
}

.container{
padding:20px;
}

.card{
background:none;
box-shadow:none;
padding:0;
}

.logo{
width:110px;
margin-bottom:20px;
}

h2{
font-weight:500;
margin-bottom:10px;
}

.subtitle{
margin-bottom:20px;
color:#666;
}

/* email input */

.input-group{
margin-bottom:20px;
}

label{
font-size:14px;
color:#333;
}

.email-row{
display:flex;
border-bottom:1px solid #605e5c;
}

input{
border:none;
flex:1;
padding:6px;
outline:none;
font-size:15px;
}

select{
border:none;
outline:none;
background:none;
font-size:15px;
cursor:pointer;
}

/* button */

.button-row{
display:flex;
justify-content:flex-end;
margin-top:20px;
}

.next{
background:#0067b8;
color:white;
border:none;
padding:8px 24px;
cursor:pointer;
}

.next:hover{
background:#005da6;
}

/* sign in text */

.signin{
margin-top:20px;
font-size:14px;
}

.signin a{
color:#0067b8;
cursor:pointer;
}


/* DESKTOP */

@media (min-width:768px){

.wrapper{
justify-content:center;
align-items:center;
background:url('../assets/background.svg');
background-size:cover;
}

.container{
max-width:440px;
width:100%;
}

.card{
background:white;
padding:44px;
border-radius:4px;
box-shadow:0 4px 20px rgba(0,0,0,0.15);
}

}

</style>