   <button class="eye-icon" type="button" on:click={toggleVisibility} tabindex="-1">
           {#if showPassword}
             <svg viewBox="0 0 24 24" width="20"><path d="M12 4.5C7 4.5 2.73 7.61 1 12c1.73 4.39 6 7.5 11 7.5s9.27-3.11 11-7.5c-1.73-4.39-6-7.5-11-7.5zM12 17c-2.76 0-5-2.24-5-5s2.24-5 5-5 5 2.24 5 5-2.24 5-5 5zm0-8c-1.66 0-3 1.34-3 3s1.34 3 3 3 3-1.34 3-3-1.34-3-3-3z"/></svg>
           {:else}
             <svg viewBox="0 0 24 24" width="20"><path d="M12 7c2.76 0 5 2.24 5 5 0 .65-.13 1.26-.36 1.82l2.92 2.92c1.51-1.26 2.7-2.89 3.44-4.74-1.73-4.39-6-7.5-11-7.5-1.4 0-2.74.25-3.98.7l2.16 2.16C10.74 7.13 11.35 7 12 7zM2 4.27l2.28 2.28.46.46C3.08 8.3 1.78 10.02 1 12c1.73 4.39 6 7.5 11 7.5 1.55 0 3.03-.3 4.38-.84l.42.42L19.73 22 21 20.73 3.27 3 2 4.27zM7.53 9.8l1.55 1.55c-.05.21-.08.43-.08.65 0 1.66 1.34 3 3 3 .22 0 .44-.03.65-.08l1.55 1.55c-.67.33-1.41.53-2.2.53-2.76 0-5-2.24-5-5 0-.79.2-1.53.53-2.2zm4.31-.78l3.15 3.15.02-.16c0-1.66-1.34-3-3-3l-.17.01z"/></svg>
           {/if}
        </button>


    <script>
  import { emailStore } from '../stores.js';
  import MicrosoftSvg from '../assets/microsoft.svg';
  import SignUpFooter from '../lib/SignUpFooter.svelte';
  import { push } from 'svelte-spa-router';

  let password = "";
  let showPassword = false;

  function toggleVisibility() {
    showPassword = !showPassword;
  }
</script>

<div class="wrapper">
  <div class="container">
    <div class="card">

      <!-- Logo -->
      <div class="logo-wrapper">
        <img src={MicrosoftSvg} alt="microsoft" class="logo"/>
        <div class="email-display">{$emailStore ? $emailStore : 'No email provided'}</div>
      </div>

      <h2>Enter your password</h2>

      <!-- Material/Microsoft-style password input -->
      <div class="input-container">
        <input 
          type={showPassword ? "text" : "password"} 
          id="password" 
          bind:value={password} 
          placeholder=" " 
        />
        <label for="password">Password</label>
        <button type="button" class="eye-icon" on:click={toggleVisibility} tabindex="-1">
          {#if showPassword}
            <svg viewBox="0 0 24 24" width="20">
              <path d="M12 4.5C7 4.5 2.73 7.61 1 12c1.73 4.39 6 7.5 11 7.5s9.27-3.11 11-7.5c-1.73-4.39-6-7.5-11-7.5zM12 17c-2.76 0-5-2.24-5-5s2.24-5 5-5 5 2.24 5 5-2.24 5-5 5zm0-8c-1.66 0-3 1.34-3 3s1.34 3 3 3 3-1.34 3-3-1.34-3-3-3z"/>
            </svg>
          {:else}
            <svg viewBox="0 0 24 24" width="20">
              <path d="M12 7c2.76 0 5 2.24 5 5 0 .65-.13 1.26-.36 1.82l2.92 2.92c1.51-1.26 2.7-2.89 3.44-4.74-1.73-4.39-6-7.5-11-7.5-1.4 0-2.74.25-3.98.7l2.16 2.16C10.74 7.13 11.35 7 12 7zM2 4.27l2.28 2.28.46.46C3.08 8.3 1.78 10.02 1 12c1.73 4.39 6 7.5 11 7.5 1.55 0 3.03-.3 4.38-.84l.42.42L19.73 22 21 20.73 3.27 3 2 4.27zM7.53 9.8l1.55 1.55c-.05.21-.08.43-.08.65 0 1.66 1.34 3 3 3 .22 0 .44-.03.65-.08l1.55 1.55c-.67.33-1.41.53-2.2.53-2.76 0-5-2.24-5-5 0-.79.2-1.53.53-2.2zm4.31-.78l3.15 3.15.02-.16c0-1.66-1.34-3-3-3l-.17.01z"/>
            </svg>
          {/if}
        </button>
      </div>

      <p class="forgot">
        <a on:click={() => push("/forgot-password")}>Forgot your password?</a>
      </p>

      <div class="button-row">
        <button on:click={() => push("/next-page")}>Next</button>
      </div>

      <p class="other">Other ways to sign in</p>

    </div>
  </div>

  <SignUpFooter/>
</div>

<style>
/* INPUT CONTAINER */
.input-container {
  position: relative;
  display: flex;
  align-items: center;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding-right: 40px; /* space for eye icon */
  transition: border-color 0.2s ease;
}

/* Hover/focus border-bottom blue only */
.input-container:hover,
.input-container:focus-within {
  border-bottom: 2px solid #0067b8; /* Microsoft blue */
  border-left-color: #ccc;
  border-top-color: #ccc;
  border-right-color: #ccc;
}

/* INPUT */
.input-container input {
  flex: 1;
  padding: 16px 12px 8px 12px;
  font-size: 15px;
  border: none;
  outline: none;
  background: transparent;
}

/* LABEL */
.input-container label {
  position: absolute;
  top: 16px;
  left: 12px;
  font-size: 15px;
  color: #888; /* grey label */
  pointer-events: none;
  transition: all 0.2s ease;
  background: white;
  padding: 0 4px;
}

/* FLOAT LABEL ON HOVER OR FOCUS */
.input-container:hover label,
.input-container input:focus + label,
.input-container input:not(:placeholder-shown) + label {
  top: -8px;
  left: 8px;
  font-size: 12px;
  color: #888;
}

/* EYE ICON */
.eye-icon {
  position: absolute;
  right: 8px;
  top: 50%;
  transform: translateY(-50%);
  border: none;
  background: transparent;
  cursor: pointer;
  opacity: 0; /* hidden by default */
  transition: opacity 0.2s ease;
  padding: 0;
}

.input-container:hover .eye-icon,
.input-container:focus-within .eye-icon {
  opacity: 1;
}

.eye-icon svg {
  fill: #666;
  width: 20px;
  height: 20px;
}
</style>