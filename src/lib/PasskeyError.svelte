<script>
import Footer from "../lib/Footer.svelte"

</script>

<div>
    <img />
    <h2> We couldn't sign you in </h2>

    <p> Something went wrong when trying to sign in with a passkey. Please try again.</p>

    <a href="#"> Learn more about passkeys </a>
    <a href="#"> Sign in another way </a>

    <div class="button-group">
        <button class="backward"> Back </button>
        <button class="forward"> Try again </button>
    </div>

    <Footer/>
</div>