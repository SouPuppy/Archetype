<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import X from '@lucide/svelte/icons/x';
  import Eye from '@lucide/svelte/icons/eye';
  import EyeOff from '@lucide/svelte/icons/eye-off';

  export let login_background = "/login_background.jpg";
  const dispatch = createEventDispatcher();

  let email = "";
  let password = "";
  let emailTouched = false;
  let showPassword = false;

  function close() {
    dispatch('close');
  }

  function getStrength(pwd: string): 'none' | 'weak' | 'medium' | 'strong' {
    if (!pwd) return 'none';
    const hasLetters = /[a-zA-Z]/.test(pwd);
    const hasNumbers = /\d/.test(pwd);
    const hasSymbols = /[^a-zA-Z0-9]/.test(pwd);
    const score = [hasLetters, hasNumbers, hasSymbols].filter(Boolean).length;
    if (pwd.length < 8 || score === 1) return 'weak';
    if (score === 2) return 'medium';
    return 'strong';
  }

  function isEmailValid(email: string): boolean {
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
  }

  $: strength = getStrength(password);
</script>

<div class="fixed inset-0 z-50 flex items-center justify-center bg-black/30 px-4">
  <div class="relative w-full max-w-2xl flex bg-white shadow-xl overflow-hidden border border-gray-200 rounded-md">
    
    <!-- Close button -->
    <button
      on:click={close}
      class="absolute top-4 right-4 text-gray-400 hover:text-blue-600 transition"
      aria-label="Close"
    >
      <X class="w-5 h-5" />
    </button>

    <!-- Left image -->
    <div
      class="hidden md:block w-[39%] bg-cover bg-center border-r border-gray-200"
      style="background-image: url({login_background});"
    ></div>

    <!-- Right form -->
    <div class="w-full md:w-[61%] px-8 py-10 flex flex-col justify-center gap-0 text-left">
      <!-- Sign Up 标题 -->
<div>
  <h2 class="text-2xl font-semibold text-gray-900 mb-1">Sign Up</h2>

  <!-- 提示/错误区域 -->
  <div class="h-[3rem] mt-3 flex transition-all duration-300">
        <p class="text-sm text-gray-500">Join InuMate and enjoy tailored video experiences</p>
  </div>
</div>
      <form class="flex flex-col gap-5">

        <!-- Email -->
        <div class="relative">
          <input
            type="text"
            placeholder="Email"
            bind:value={email}
            autocomplete="off"
            autocorrect="off"
            autocapitalize="off"
            spellcheck={false}
            on:blur={() => (emailTouched = true)}
            class="peer text-sm px-1 py-0.5 border-b border-gray-300 outline-none w-full transition"
          />

          <div class="absolute left-0 bottom-0 w-full h-[2px] scale-x-0 peer-hover:scale-x-100 peer-focus:scale-x-100 transition-transform origin-left bg-blue-600"></div>

{#if email}
  <button
    type="button"
    on:mousedown|preventDefault
    on:click={() => {
      email = "";
      emailTouched = false;
    }}
    class="absolute right-1 top-1/2 transform -translate-y-1/2 p-1 text-gray-500 hover:text-gray-600 group"
  >
    <X class="w-4 h-4 stroke-[1.5] group-hover:stroke-[2]" />
  </button>
{/if}

        </div>

        <!-- Password -->
        <div class="relative">
          <input
            type={showPassword ? 'text' : 'password'}
            placeholder="Password"
            bind:value={password}
            class="peer text-sm px-1 py-0.5 border-b border-gray-300 
                   outline-none w-full pr-8 transition"
          />

          <div class="absolute left-0 bottom-0 w-full h-[2px] scale-x-0 peer-hover:scale-x-100 peer-focus:scale-x-100 transition-transform origin-left bg-blue-600"></div>

          <!-- Toggle password -->
          <button
            type="button"
            class="absolute right-1 top-1/2 transform -translate-y-1/2 p-1 text-gray-500 hover:text-gray-600 group"
            on:click={() => (showPassword = !showPassword)}
            aria-label="Toggle password visibility"
          >
            {#if showPassword}
              <EyeOff class="w-4 h-4 stroke-[1.5] group-hover:stroke-[2]" />
            {:else}
              <Eye class="w-4 h-4 stroke-[1.5] group-hover:stroke-[2]" />
            {/if}
          </button>

          <!-- Strength bar -->
          <div
            class="absolute left-0 bottom-[-6px] h-[4px] transition-all duration-300"
            style="
              width: {
                strength === 'none' ? '0%' :
                strength === 'weak' ? '20%' :
                strength === 'medium' ? '40%' : '100%'
              };
              background-color: {
                strength === 'none' ? 'transparent' :
                strength === 'weak' ? '#f87171' :
                strength === 'medium' ? '#facc15' : '#4ade80'
              };
            "
          ></div>
        </div>

        <!-- Submit -->
        <button
          type="submit"
          class="mt-2 bg-blue-600 hover:bg-blue-700 text-white text-sm font-semibold py-2 transition rounded"
        >
          Sign Up
        </button>
      </form>

      <!-- Legal links -->
      <div class="text-sm text-gray-500 mt-10 mb-[-1rem]">
        Already have an account?
        <a href=" " class="text-blue-600 underline">Login</a><br />
        By signing up, you agree to our
        <a href="#" class="text-blue-600 underline"> Terms </a> and
        <a href="#" class="text-blue-600 underline"> Privacy </a>.
      </div>
    </div>
  </div>
</div>
