<script>
import Router from "svelte-spa-router";

import Loading from "./lib/Loading.svelte";
import LoginEmailPage from "./lib/LoginEmailPage.svelte";
import SignInOptions from "./lib/SignInOptions.svelte";
import LoginPasswordPage from "./lib/LoginPasswordPage.svelte"
// import SignUp from "./lib/SignUp.svelte";
import ErrorPage from "./lib/ErrorPage.svelte";

const routes = {
  "/": Loading,
  "/login": LoginEmailPage,
  "/signin-options": SignInOptions,
  "/error": ErrorPage,
  '/enter-your-password': LoginPasswordPage,
};
</script>

<Router {routes} />