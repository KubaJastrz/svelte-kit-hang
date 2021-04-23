<script context="module" lang="ts">
  export const prerender = true
</script>

<script lang="ts">
  import {useQuery} from '@sveltestack/svelte-query'

  let joke: string[] | undefined

  const query = useQuery('joke', {
    queryFn: () =>
      fetch('https://official-joke-api.appspot.com/random_joke').then((data) => data.json()),
  })

  $: {
    if ($query.data) {
      joke = [$query.data.setup, $query.data.punchline]
    }
  }
</script>

<svelte:head>
  <title>Home</title>
</svelte:head>

{#if joke}
  <p>{joke[0]}</p>
  <p>{joke[1]}</p>
{/if}
