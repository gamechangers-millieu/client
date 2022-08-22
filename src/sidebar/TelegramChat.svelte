<!-- https://stackoverflow.com/questions/59629947/how-do-i-load-an-external-js-library-in-svelte-sapper -->
<!-- https://core.telegram.org/widgets/discussion -->
<div>
  <script async 
  bind:this={script}
  src="{url}" 
  data-telegram-discussion="{post}" 
  data-comments-limit="5" 
  data-height="300"
  data-color="343638" 
  data-dark="1"
  data-dark-color="FFFFFF"
  />

</div>

<script>
  import { onMount, createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();
  
  export let post
  let url = "https://telegram.org/js/telegram-widget.js?19";
  let script = "https://telegram.org/js/telegram-widget.js?19";

  onMount(async () => {
    script.addEventListener('load', () => {
      dispatch('loaded');
    })

    script.addEventListener('error', (event) => {
      console.error("something went wrong", event);
      dispatch('error');
    });
  });
</script>
