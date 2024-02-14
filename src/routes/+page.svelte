<script>
  // toggle layout

  import UserData from "./userData.svelte";

  let layout = "signIn";
  let btnText = "Sign in";

  let submitted = false;

  const toggleForm = (className, text) => {
    layout = className;
    btnText = text;
  };

  // Validation

  export let data = {
    email: "",
    password1: "",
    password2: "",
  };

  let emailErrorMessage = "";
  let password1ErrorMessage = "";
  let password2ErrorMessage = "";

  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

  const validateEmail = (e) => {
    if (e === "" || !emailRegex.test(e)) {
      emailErrorMessage = "Please enter a valid email";
    } else {
      data.email = e;
      emailErrorMessage = "";
    }
  };

  const validatePassword = (e) => {
    if (e === "" || e.length < 6) {
      password1ErrorMessage = "Please enter a password";
      console.log(password1ErrorMessage);
    } else {
      data.password1 = e;
      password1ErrorMessage = "";
      console.log(data);
    }
  };

  const validatePassword2 = (e) => {
    if (e === "" || e !== data.password1) {
      password2ErrorMessage = "Passwords do not match";
      console.log(password2ErrorMessage);
    } else {
      data.password2 = e;
      password2ErrorMessage = "";
      console.log(data);
    }
  };
</script>

<div style="background-color: #019ef7">
  <div
    class="container-sm d-flex justify-content-center align-items-center vh-100"
  >
    {#if submitted === false}
      <form
        id="form"
        class={`d-flex flex-column p-4 rounded-4 justify-content-center shadow-lg bg-light ${layout} `}
        style="min-width: 22rem; min-height: 42rem"
        on:submit={(e) => {
          e.preventDefault();
          submitted = true;
        }}
      >
        <div class="my-5 d-flex flex-column align-items-start">
          <button
            type="button"
            id="signInBtn"
            class="btn btn-white text-primary fs-1 fw-bold p-0 {layout ===
            'signUp'
              ? 'opacity-50'
              : ''}"
            on:click={() => toggleForm("signIn", "Sign in")}
          >
            Sign in
          </button>
          <button
            type="button"
            id="signupBtn"
            class="btn btn-white text-primary fs-1 fw-bold p-0 {layout ===
            'signIn'
              ? 'opacity-50'
              : ''}"
            on:click={() => toggleForm("signUp", "Sign Up")}
          >
            Sign Up
          </button>
        </div>
        <div class="mt-3 w-100">
          <input
            type="Email"
            class="form-control rounded-4"
            id="email"
            aria-describedby="emailHelp"
            placeholder="Enter email"
            on:blur={(e) => validateEmail(e.target.value)}
          />
          <div
            id="error"
            class="text-danger ms-2 text-start"
            style="font-size: 0.8rem"
          >
            {emailErrorMessage}
          </div>
        </div>
        <div class="mt-3">
          <input
            type="password"
            class="form-control rounded-4"
            id="password1"
            placeholder="Password"
            on:blur={(e) => validatePassword(e.target.value)}
          />
          <div
            id="error"
            class="text-danger ms-2 text-start"
            style="font-size: 0.8rem"
          >
            {password1ErrorMessage}
          </div>
        </div>
        {#if layout === "signUp"}
          <div class="mt-3">
            <input
              type="password"
              class="form-control rounded-4"
              id="password2"
              placeholder="Verify Password"
              on:blur={(e) => validatePassword2(e.target.value)}
            />
            <div
              id="error"
              class="text-danger ms-2 text-start"
              style="font-size: 0.8rem"
            >
              {password2ErrorMessage}
            </div>
          </div>
        {/if}
        <p id="forgotPass" class="text-end my-4 fs-6">
          <a
            href="#"
            class="link-primary fw-bold link-offset-2 link-opacity-75 link-underline-opacity-0 link-underline-opacity-100-hover"
            >Forgot Password</a
          >
        </p>
        <button
          type="submit"
          id="submitBtn"
          class="btn btn-primary rounded-5 my-5 {emailErrorMessage !== '' ||
          password1ErrorMessage !== '' ||
          password2ErrorMessage !== ''
            ? 'disabled'
            : ' '}"
        >
          {btnText}
        </button>
        <p class="text-center mb-4 fs-6">
          <a
            href="#"
            class="link-primary fw-bold link-offset-2 link-underline-no link-underline-opacity-100-hover"
            >Privacy Policy</a
          >
        </p>
      </form>
    {:else}
      <UserData {data} />
    {/if}
  </div>
</div>
