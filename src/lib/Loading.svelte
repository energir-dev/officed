<script>
import { onMount } from "svelte";
import { push } from "svelte-spa-router";

import MicrosoftSvg from '../assets/microsoft.svg';
import Animation from '../lib/LoadingAnimation.svelte';

onMount(() => {
  setTimeout(() => {
    push("/login");
  }, 3000);
});
</script>

<div class="loading-container">

  <div class="card">
      <img src={MicrosoftSvg} alt="microsoft" id="MSLogo"/>

      <h2>Trying to sign you in...</h2>

      <Animation/>
  </div>

</div>

<style>

/* MOBILE FIRST */

.loading-container {
    min-height: 100vh;
    width: 100%;
    background: white;

    display: flex;
    justify-content: flex-start;
    align-items: flex-start;

    padding: 20px;
}

/* remove card look on mobile */

.card{
    background: none;
    box-shadow: none;
    padding: 0;
    text-align: left;
}

/* logo */

#MSLogo{
    width: 120px;
    margin-bottom: 20px;
}

/* text */

h2{
    font-size: 22px;
    font-weight: 500;
    margin-bottom: 20px;
}


/* DESKTOP */

@media (min-width:768px){

.loading-container{
    justify-content: center;
    align-items: center;

    background-image: url("../assets/background.svg");
    background-size: cover;
    background-position: center;
}

/* restore card */

.card{
    background: white;
    color: black;
    padding: 40px;
    border-radius: 6px;
    text-align: center;

    box-shadow: 0 10px 30px rgba(0,0,0,0.2);

    max-width: 420px;
    width: 100%;
}

}

</style>