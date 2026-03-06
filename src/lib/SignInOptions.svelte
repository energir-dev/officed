<script>
import Picker from '../assets/picker_account.svg';
import Account from '../assets/account.svg';
import MicrosoftSvg from '../assets/microsoft.svg';
import { push } from "svelte-spa-router";

</script>

<div class="wrapper">

<div class="container">

<div class="card">

<img src={MicrosoftSvg} alt="microsoft" class="logo"/>

<h2>Which type of account do you need help with?</h2>

<div class="option"on:click={()=> push("/error")}> 

<img src={Picker} alt="picker"/>

<div>
<h4>Work or school account</h4>
<p>Created by your IT department</p>
</div>

</div>

<div class="option" on:click={()=> push("/error")}>

<img src={Account} alt="account"/>

<div>
<h4>Personal account</h4>
<p>Created by you</p>
</div>

</div>

<div class="button-row">
<button on:click={()=> {push("/login")}}>Back</button>
</div>

</div>

</div>

</div>

<style>

/* MOBILE FIRST */

.wrapper{
min-height:100vh;
background:white;
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
font-size:22px;
margin-bottom:20px;
}

/* options */

.option{
display:flex;
gap:15px;
align-items:flex-start;
margin-bottom:20px;
cursor:pointer;
}

.option img{
width:28px;
}

.option h4{
margin:0;
font-weight:600;
}

.option p{
margin:4px 0 0;
font-size:14px;
color:#666;
}

/* button */

.button-row{
display:flex;
justify-content:flex-end;
margin-top:20px;
}

button{
background: #D3D3D3;
color: #000033;
border:none;
padding:8px 24px;
cursor:pointer;
}

button:hover {
    transform: scale(1.01);
}

button:hover, button:focus {
    outline: none;
}

/* DESKTOP */

@media (min-width:768px){

.wrapper{
display:flex;
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