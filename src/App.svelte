<script>
  import { fade, fly, scale } from "svelte/transition";
  import { bounceIn } from "svelte/easing";
  import Loader from "./lib/Loader.svelte";
  let click = false, vid;
  let removeimg = false
  let loader = false;
  const clicked = () => {
    loader = true
    setTimeout(()=>{
      removeimg = true;
      click = false
    }, 7000)
  };
  const blackfull = () => {
      if (vid.requestFullscreen) {
        vid.requestFullscreen();
      }
  }
</script>

<!-- svelte-ignore a11y_click_events_have_key_events -->
<!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
 {#if !removeimg}
 <img on:click={()=>click = true} src="./shop.png" class="w-[100vw] h-[100vh] object-contain" alt="Free" />
 {/if}
<!-- svelte-ignore a11y_media_has_caption -->
<!-- svelte-ignore a11y_consider_explicit_label -->
<button bind:this={vid} class="bg-black w-[100vw] h-[100vh] m-0 p-0 block" on:click={blackfull}></button>
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
    class="absolute h-fit left-1/2 -translate-x-1/2 top-[5%] bg-white w-3/4 sm:w-[550px] rounded-2xl z-[99] overflow-y-auto flex flex-col"
  >
    <div class="flex items-center justify-center">
      <h1 class="text-4xl font-bold p-4 pt-6 text-black">You won a free iPhone</h1>
    </div>
    <hr />
    <div class="p-14 pb-4 pt-0 text-center text-black text-3xl">
      <img src="https://powermaccenter.com/cdn/shop/files/iPhone_16_Pro_Desert_Titanium_PDP_Image_Position_1__en-WW_a9715438-f77d-4048-994a-1a4506ccabda.jpg?v=1726237380" class=" mx-auto" alt="">
      🎉 Congratulations! Ikaw ang ika-100,000th visitor! Manalo ng LIBRENG iPhone!📱🎊
    </div>
    <hr />
    <div class="flex w-1/2 mx-auto gap-4 p-4">
      <button class="btn btn-primary text-2xl flex-1" on:click={clicked}
        >{#if loader}<Loader />{:else}Claim{/if}</button
      >
    </div>
  </div>
</div>
{/if}
<style>
</style>
