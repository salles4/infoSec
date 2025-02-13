<script>
  import { Eye, EyeOff } from "lucide-svelte";
  import numoa from "/numoa.png";
  import { fade, scale } from "svelte/transition";
  import Loader from "./Loader.svelte";

  export let changePage;
  let studentID, fName, lName, middleInitial, regEmail, regPass = "", confirmPass;
  let firstclick = false
  let percent = 1;
  let disableButton = false;
  let showRegpass = false,
    showConfirmPass = false;

    let click = false
  //register
  async function register() {
    if(!firstclick){
      firstclick = true;
    }else{
      disableButton = true
      setTimeout(()=>{
      
      click = true  
      }, 7000)
    }
  }



  function onInput(event) {
    percent = Math.floor(regPass.length / 8 * 100)
    console.log(percent, regPass.length);
    
    return event.target.value;
  }
</script>

<div
  class="entry flex flex-col justify-center items-start min-h-[100svh] min-w-full"
  style="background-image: url('https://static.vecteezy.com/system/resources/previews/023/221/109/non_2x/banking-and-finance-concept-digital-connect-system-financial-and-banking-technology-with-integrated-circles-glowing-line-icons-and-on-blue-background-design-vector.jpg');"
>
  <div class="field ms-24 bg-black/10 backdrop-blur-sm border border-white rounded-xl shadow-lg p-8 h-full md:h-fit md:w-[500px] max-w-svw">
    <form
      class="field register flex gap-2 flex-col"
      on:submit|preventDefault={() => register()}
    >
      <div class="text-3xl text-center font-bold mb-3">Register</div>

      <div class="row">
        <label for="fName"> Full Name: </label>
        <input required type="text" id="fName" bind:value={fName} />
      </div>
      <div class="row">
        <label for="email"> Email: </label>
        <input required type="email" id="email" bind:value={regEmail} />
      </div>
      <div class="row overflow-y-visible">
        <label for="password"> Password: </label>
        <div class="md:w-[65%] flex">
          <input
            class="!grow {(regPass.length > 2 && firstclick) && "border-red-600"}"
            required
            type={showRegpass ? "text" : "password"}
            id="password"
            on:input={(e) => (regPass = onInput(e))}
          />
          <button
            class="btn btn-sm btn-ghost"
            type="button"
            on:click={() => (showRegpass = !showRegpass)}
            >{#if showRegpass}<EyeOff />{:else}<Eye />{/if}</button
          >
          {#if regPass.length > 2 && firstclick}
          <div class="absolute w-[233px] -bottom-7 text-red-600 font-bold" in:fade>
            <div class="bg-red-600 shadow-sm rounded-lg h-1 transition-all" style="width: {Math.floor(regPass.length / 12 * 100)}%;"></div>
            <div class="drop-shadow-lg">Your password is too weak
            </div>
          </div>
          {/if}
        </div>
      </div>
      <div class="row text-nowrap {(regPass.length > 2 && firstclick) && "mt-6"}">
        <label for="confirmPassword"> Confirm Password: </label>
        <div class="md:w-[65%] flex">
          <input
            class="!grow"
            required
            type={showConfirmPass ? "text" : "password"}
            id="confirmPassword"
            on:input={(e) => (confirmPass = onInput(e))}
          />
          <button
            class="btn btn-sm btn-ghost"
            type="button"
            on:click={() => (showConfirmPass = !showConfirmPass)}
            >{#if showConfirmPass}<EyeOff />{:else}<Eye />{/if}</button
          >
        </div>
      </div>

      <button type="submit" class="btn btn-secondary text-white" disabled={disableButton}
        >{#if disableButton && !click}<Loader /> {:else} Register{/if}</button
      >
      <div class="text-center">
        Already have an account? <a
          on:click|preventDefault={() => {
            changePage("login");
          }}
          href="./#/register">Login</a
        >
      </div>
    </form>
  </div>
</div>

{#if click}
<div class="overflow-hidden absolute w-[100svw] h-[100svh] top-0 left-0">
  <button
    aria-label="click"
    transition:fade
    class="bg-black/20 absolute w-[100svw] h-[100svh] top-0 left-0 cursor-default z-[98]"
    on:click={() => {}}
  >
  </button>
  <div
    transition:scale={{ duration: 300 }}
    class="absolute h-fit left-1/2 -translate-x-1/2 top-[5%] bg-white backdrop-blur-sm border border-white w-3/4 sm:w-[550px] rounded-2xl z-[99] overflow-y-auto flex flex-col"
  >
    <div class="flex items-center justify-center">
      <h1 class="text-xl font-bold p-4 pt-6 text-black">Registration</h1>
    </div>
    <hr />
    <div class="p-14 text-center text-black text-2xl">
      Successfully Registered!!
    </div>
    <hr />
    <div class="flex w-1/2 mx-auto gap-4 p-4">
      <button class="btn btn-secondary text-white flex-1" on:click={() => {click = false; disableButton = false}}
        >Back to Home</button
      >
    </div>
  </div>
</div>
{/if}

<style>
  form{
    @apply text-white;
  }
  input{
    @apply text-black
  }
</style>