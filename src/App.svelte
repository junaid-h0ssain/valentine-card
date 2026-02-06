<script>
    // In Svelte 5, we use $state() for variables that update the screen
    let showSuccess = $state(false);
    let noBtnPosition = $state({ left: "50%", top: "50%" });
    let isNoBtnMoved = $state(false);
    let currentMessage = $state("Will you be my Valentine? 💖");

    const hoverMessages = [
        "Why?",
        "No...",
        "Plssss",
        "Come on!",
        "Think again",
        "Really?",
        "Are you sure?",
        "Don't be shy 💕",
        "Please???",
        "You're breaking my heart 💔",
    ];

    function moveButton() {
        // 1. Change Text
        const randomMsg =
            hoverMessages[Math.floor(Math.random() * hoverMessages.length)];
        currentMessage = randomMsg;

        // 2. Move Button
        const maxWidth = window.innerWidth - 150; // Ensure it fits on screen
        const maxHeight = window.innerHeight - 60;

        // Math.max ensures we don't get negative numbers on small phones
        const randomX = Math.random() * Math.max(0, maxWidth);
        const randomY = Math.random() * Math.max(0, maxHeight);

        noBtnPosition = { left: `${randomX}px`, top: `${randomY}px` };
        isNoBtnMoved = true;
    }
</script>

<main>
    <div class="container">
        {#if !showSuccess}
            <div id="question-section">
                <h1>{currentMessage}</h1>
                <div class="buttons">
                    <button id="yesBtn" onclick={() => (showSuccess = true)}
                        >Yes!</button
                    >

                    <button
                        id="noBtn"
                        onmouseenter={moveButton}
                        onclick={moveButton}
                        style:position={isNoBtnMoved ? "fixed" : "relative"}
                        style:left={noBtnPosition.left}
                        style:top={noBtnPosition.top}
                    >
                        No
                    </button>
                </div>
            </div>
        {:else}
            <div class="gif-container">
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
        background-color: #f0f0f0;
        color: #333;
        position: relative;
    }

    /* Image for the celebration state */
    .gif-container img {
        max-width: 100%;
        border-radius: 10px;
    }
</style>

