<script>
import MicrosoftSvg from '../assets/microsoft.svg';
import Footer from './Footer.svelte';
import { push } from "svelte-spa-router";
</script>

<div class="wrapper">

<div class="container">

<div class="card">

<img src={MicrosoftSvg} alt="microsoft" class="logo"/>

<h2>Sign in</h2>

<p class="error">
Sorry, but we're having trouble signing you in.
</p>

<p class="hint">
Please try again or return to the sign-in page.
</p>

<div class="button-row">
<button on:click={() => push('/login')}>
Back to sign in
</button>
</div>

</div>

</div>

<Footer/>

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

.error{
font-size:16px;
margin-bottom:10px;
}

.hint{
font-size:14px;
color:#666;
margin-bottom:20px;
}

/* button */

.button-row{
display:flex;
justify-content:flex-end;
margin-top:20px;
}

button{
background:#0067b8;
color:white;
border:none;
padding:8px 24px;
cursor:pointer;
}

button:hover{
background:#005da6;
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