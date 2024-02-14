<script>
  export let data = {};
</script>

<div
  class={`d-flex flex-column p-4 rounded-4 justify-content-center shadow-lg bg-light`}
>
  <h1 class="my-4">User Data:</h1>
  <p class="fs-4 fw-bold p-0">
    Email: <span class="fs-4 fw-bold p-0 text-primary">{data.email}</span>
  </p>
  <p class="fs-4 fw-bold p-0">
    Password: <span class="fs-4 fw-bold p-0 text-primary">{data.password1}</span
    >
  </p>
  <p class="fs-4 fw-bold p-0">
    Confirm Password: <span class="fs-4 fw-bold p-0 text-primary"
      >{data.password2}</span
    >
  </p>
</div>
