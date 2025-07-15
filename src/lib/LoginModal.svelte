<!-- Login Step UI: 调整步骤圆圈垂直居中位置，并强制以右对齐为基准布局 -->
<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import X from '@lucide/svelte/icons/x';

   let login_background = ""; //"/login_background.jpg";
  const dispatch = createEventDispatcher();

  let email = "";
  let password = "";

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

  $: strength = getStrength(password);
</script>

<div class="fixed inset-0 z-50 flex items-center justify-center bg-black/30 px-4">
  <div class="relative w-full max-w-2xl flex bg-white shadow-xl overflow-hidden border border-gray-200 rounded-md">

    <!-- 关闭按钮 -->
    <button
      on:click={close}
      class="absolute top-4 right-4 text-gray-400 hover:text-blue-600 transition"
      aria-label="Close"
    >
      <X class="w-5 h-5" />
    </button>

    <!-- 左图区域 -->
    <div
      class="hidden md:block w-[35%] bg-cover bg-center border-r border-gray-200"
      style="background-image: url({login_background});"
    ></div>

    <!-- 中间步骤条 -->
    <div class="absolute left-[calc(9%)] top-0 bottom-0 flex items-center">
      <div class="flex flex-col items-end justify-center h-full px-4">
        <div class="flex items-center gap-3 mb-8">
          <div class="text-sm text-right">
            <div class="font-medium text-black">Finished</div>
            <div class="text-gray-400">This is a description.</div>
          </div>
          <div class="relative flex flex-col items-center">
            <div class="w-6 h-6 rounded-full bg-blue-100 flex items-center justify-center text-blue-600 font-semibold text-sm z-10">
              ✓
            </div>
            <div class="h-10 w-0.5 bg-blue-600"></div>
          </div>
        </div>
        <div class="flex items-center gap-3 mb-8">
          <div class="text-sm text-right">
            <div class="font-medium text-black">In Progress</div>
            <div class="text-gray-400">This is a description.</div>
          </div>
          <div class="relative flex flex-col items-center">
            <div class="w-6 h-6 rounded-full bg-blue-600 text-white flex items-center justify-center font-semibold text-sm z-10">2</div>
            <div class="h-10 w-0.5 bg-gray-300"></div>
          </div>
        </div>
        <div class="flex items-center gap-3">
          <div class="text-sm text-right">
            <div class="font-medium text-gray-400">Waiting</div>
            <div class="text-gray-300">This is a description.</div>
          </div>
          <div class="relative flex flex-col items-center">
            <div class="w-6 h-6 rounded-full bg-gray-200 text-gray-500 flex items-center justify-center font-semibold text-sm z-10">3</div>
          </div>
        </div>
      </div>
    </div>

    <!-- 右侧表单区域 -->
    <div class="w-full md:w-[65%] px-8 py-10 flex flex-col justify-center gap-6 text-left ml-auto">
      <div>
        <h2 class="text-2xl font-semibold text-gray-900 mb-1">Sign Up</h2>
        <p class="text-sm text-gray-500">Join InuMate and enjoy tailored video experiences</p>
      </div>

      <form class="flex flex-col gap-4">
        <div class="relative">
          <input
            type="text"
            placeholder="Email"
            bind:value={email}
            autocomplete="off"
            autocorrect="off"
            autocapitalize="off"
            spellcheck={false}
            class="text-sm px-1 py-0.5 border-b border-gray-300 hover:border-b-[2px] focus:border-blue-600 hover:border-blue-500 outline-none transition w-full"
          />
          {#if email}
            <button
              type="button"
              on:click={() => (email = "")}
              class="absolute right-1 top-1/2 transform -translate-y-1/2 p-1 text-gray-500 hover:text-gray-600 group"
            >
              <X class="w-4 h-4 stroke-[1.5] group-hover:stroke-[2]" />
            </button>
          {/if}
        </div>

        <div class="relative">
          <input
            type="password"
            placeholder="Password"
            bind:value={password}
            class="text-sm px-1 py-0.5 border-b border-gray-300 hover:border-b-[2px] focus:border-blue-600 hover:border-blue-500 outline-none transition w-full"
          />
          <div
            class="absolute left-0 bottom-[-6px] h-[4px] transition-all duration-300"
            style="
              width: {
                strength === 'none' ? '0%' :
                strength === 'weak' ? '33.3%' :
                strength === 'medium' ? '66.6%' : '100%'
              };
              background-color: {
                strength === 'none' ? 'transparent' :
                strength === 'weak' ? '#f87171' :
                strength === 'medium' ? '#facc15' : '#4ade80'
              };
            "
          ></div>
        </div>

        <button
          type="submit"
          class="bg-blue-600 hover:bg-blue-700 text-white text-sm font-semibold py-2 transition rounded"
        >
          Sign Up
        </button>
      </form>

      <div class="text-sm text-gray-500">
        Already have an account?
        <a href="#" class="text-blue-600 underline">Login</a><br />
        By signing up, you agree to our
        <a href="#" class="text-blue-600 underline"> Terms </a> and
        <a href="#" class="text-blue-600 underline"> Privacy </a>.
      </div>
    </div>
  </div>
</div>
