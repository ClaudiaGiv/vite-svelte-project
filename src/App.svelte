<script>
  import { auth } from './go-true';
  // import { goto } from '$app/navigation';

  let username = '';
  let password1 = '';
  let password2 = '';
  let usernameError = false;
  let passwordError = false;
  async function signUp() {
    if (username === '') {
      usernameError = true;
      return;
    }
    if (password1 === '' || password2 === '') {
      passwordError = true;
      return;
    }
    usernameError = false;
    passwordError = false;
    auth
            .signup(username, password1)
            .then((response) => {
              console.log('Confirmation email sent', response);
              // goto('/');
            })
            .catch((error) => console.log("It's an error", error));
  }
  $: console.log(username);
  $: console.log(password1);
  $: console.log(password2);
</script>

<h1>Register</h1>
<div class="w-full max-w-xs mx-auto mt-4">
  <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
    <div class="mb-4">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="username"> Username </label>
      <input
              class:border-red-500={usernameError && username === ''}
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="username"
              type="text"
              placeholder="Username"
              bind:value={username}
      />
      {#if usernameError && username === ''}
        <p class="text-red-500 text-xs italic">Please provide a valid username.</p>
      {/if}
    </div>
    <div class="mb-6">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="password1"> Password </label>
      <input
              class:border-red-500={passwordError && password1 === ''}
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
              id="password1"
              type="password"
              placeholder="******************"
              bind:value={password1}
      />
      {#if passwordError && password1 === ''}
        <p class="text-red-500 text-xs italic">Please provide a valid password.</p>
      {/if}
    </div>
    <div class="mb-6">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="password2">
        Confirm password
      </label>
      <input
              class:border-red-500={passwordError && password2 === ''}
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
              id="password2"
              type="password"
              placeholder="******************"
              bind:value={password2}
      />
      {#if passwordError && password2 === ''}
        <p class="text-red-500 text-xs italic">Please provide a valid password.</p>
      {/if}
    </div>
    <div class="flex items-center justify-between">
      <button
              class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-2 rounded focus:outline-none focus:shadow-outline"
              type="button"
              on:click={signUp}
      >
        Sign Up
      </button>
      <a
              class="inline-block align-baseline font-bold text-sm text-blue-500 hover:text-blue-800"
              href="/login"
      >
        Already have an account?
      </a>
    </div>
  </form>
</div>
