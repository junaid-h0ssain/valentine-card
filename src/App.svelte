<script>
  import { onMount } from 'svelte';

  let showSuccess = false;
  let noBtnPosition = { left: 'auto', top: 'auto' };
  let isNoBtnMoved = false;

  onMount(() => {
    // Initial position can be set here if needed
  });

  function moveButton() {
    const windowWidth = window.innerWidth;
    const windowHeight = window.innerHeight;
    const btnWidth = 100; // Approximate button width
    const btnHeight = 50; // Approximate button height

    const randomX = Math.random() * (windowWidth - btnWidth - 50);
    const randomY = Math.random() * (windowHeight - btnHeight - 50);

    noBtnPosition = { left: randomX + 'px', top: randomY + 'px' };
    isNoBtnMoved = true;
  }

  function handleYes() {
    showSuccess = true;
  }
</script>

<main>
  <div class="container">
    {#if !showSuccess}
      <div id="question-section">
        <h1>Will you be my Valentine? 💖</h1>
        <div class="buttons">
          <button id="yesBtn" on:click={handleYes}>Yes!</button>
          <button
            id="noBtn"
            on:mouseover={moveButton}
            on:click={moveButton}
            style={isNoBtnMoved ? `position: fixed; left: ${noBtnPosition.left}; top: ${noBtnPosition.top};` : ''}
          >
            No
          </button>
        </div>
      </div>
    {:else}
      <div id="success-section" class="gif-container">
        <h1>Yay! I knew it! 🥰</h1>
        <img
          src="https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExb2xrMGQzdno1c2tvZ3NxZmw5ZjNncHlwMjY3emE3ZnBrMHJudW1xMiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/IqojY0rgVWfOE/giphy.gif"
          alt="Cute bear hug"
        />
      </div>
    {/if}
  </div>
</main>

<style>
  body {
    margin: 0;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #ffe6e9; /* Light pink background */
    font-family: "Arial", sans-serif;
    overflow: hidden; /* Prevents scrollbars when button moves */
  }

  .container {
    text-align: center;
    background: white;
    padding: 40px;
    border-radius: 20px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
    max-width: 90%;
    position: relative;
  }

  h1 {
    color: #ff4d6d;
    font-size: 2.5rem;
    margin-bottom: 30px;
  }

  .buttons {
    display: flex;
    justify-content: center;
    gap: 20px;
    position: relative; /* Needed for button positioning context if you want it contained */
  }

  button {
    padding: 15px 30px;
    font-size: 1.2rem;
    border: none;
    border-radius: 50px;
    cursor: pointer;
    transition: transform 0.2s;
  }

  #yesBtn {
    background-color: #ff4d6d;
    color: white;
    font-weight: bold;
  }

  #yesBtn:hover {
    background-color: #d63352;
    transform: scale(1.1);
  }

  #noBtn {
    background-color: #f5a2a2;
    color: #eaa2a2;
    position: relative;
  }

  /* Image for the celebration state */
  .gif-container img {
    max-width: 100%;
    border-radius: 10px;
  }
</style>
