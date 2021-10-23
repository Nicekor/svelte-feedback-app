<script lang="ts">
  import { v4 } from 'uuid'
  import { Feedback, FeedbackStore } from '../stores'
  import RatingSelect from './RatingSelect.svelte'
  import Button from './UI/Button.svelte'
  import Card from './UI/Card.svelte'

  let text = ''
  let rating = 10
  let btnDisabled = true
  let min = 10
  let message = ''

  const handleSelect = (e: CustomEvent<number>) => (rating = e.detail)

  const handleInput = () => {
    if (text.trim().length <= min) {
      message = `Text must be at least ${min} characters`
      btnDisabled = true
    } else {
      message = ''
      btnDisabled = false
    }
  }

  const handleSubmit = () => {
    if (text.trim().length > min) {
      const newFeedback: Feedback = {
        id: v4(),
        text,
        rating,
      }
      FeedbackStore.update((feedback) => [newFeedback, ...feedback])
      text = ''
    }
  }
</script>

<Card>
  <header>
    <h2>How would you rate your service with us?</h2>
  </header>
  <form on:submit|preventDefault={handleSubmit}>
    <RatingSelect on:rating-select={handleSelect} />
    <div class="input-group">
      <input
        type="text"
        on:input={handleInput}
        bind:value={text}
        placeholder="Tell us something that keeps you coming back"
      />
      <Button disabled={btnDisabled} type="submit">Send</Button>
    </div>
    {#if message}
      <div class="message">
        {message}
      </div>
    {/if}
  </form>
</Card>

<style>
  header {
    max-width: 400px;
    margin: auto;
  }
  header h2 {
    font-size: 22px;
    font-weight: 600;
    text-align: center;
  }
  .input-group {
    display: flex;
    flex-direction: row;
    border: 1px solid #ccc;
    padding: 8px 10px;
    border-radius: 8px;
    margin-top: 15px;
  }
  input {
    flex-grow: 2;
    border: none;
    font-size: 16px;
  }
  input:focus {
    outline: none;
  }
  .message {
    padding-top: 10px;
    text-align: center;
    color: rebeccapurple;
  }
</style>
