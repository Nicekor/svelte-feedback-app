<script lang="ts">
  // import { onDestroy, onMount } from 'svelte'
  import { fade, scale } from 'svelte/transition'
  import { FeedbackStore } from '../stores'
  // import type { Feedback } from '../stores'
  import FeedbackItem from './FeedbackItem.svelte'

  // let feedback: Feedback[]

  // const unsubscribe = FeedbackStore.subscribe((data) => (feedback = data))

  // onMount(() => {
  //   console.log('mounted')
  // })

  // onDestroy(() => {
  //   unsubscribe()
  // })
</script>

{#each $FeedbackStore as fb (fb.id)}
  <div in:scale out:fade={{ duration: 500 }}>
    <FeedbackItem item={fb} />
  </div>
{/each}
