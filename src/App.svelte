<script>
import Router from "svelte-spa-router";

import Loading from "./lib/Loading.svelte";
import LoginEmailPage from "./lib/LoginEmailPage.svelte";
import SignInOptions from "./lib/SignInOptions.svelte";
import LoginPasswordPage from "./lib/LoginPasswordPage.svelte"
// import SignUp from "./lib/SignUp.svelte";
import ErrorPage from "./lib/ErrorPage.svelte";
import LoginOtpPage from "./lib/LoginOtpPage.svelte";
import GetACode from "./lib/GetACode.svelte";

const routes = {
  "/": Loading,
  "/login": LoginEmailPage,
  "/otp": LoginOtpPage,
  "/signin-options": SignInOptions,
  "/error": ErrorPage,
  '/enter-your-password': LoginPasswordPage,
  '/choose-option': GetACode,
};
</script>

<Router {routes} />