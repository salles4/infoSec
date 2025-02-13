<script>
  import Routes, { location, replace } from "svelte-spa-router";
  import Iphone from "./lib/Iphone.svelte";
  import Password from "./lib/Password.svelte";
  import Home from "./lib/Home.svelte";
  
</script>

<Routes routes={{
  "/":Home,
  "/iphone": Iphone,
  "/password": Password
}} />