<script>
    // In Svelte 5, we use $state() for variables that update the screen
    let showSuccess = $state(false);
    let noBtnPosition = $state({ left: "auto", top: "auto" });
    let isNoBtnMoved = $state(false);
    let currentMessage = $state("Will you be my Valentine? 💖");
    let container;

    const hoverMessages = [
        "Why?",
        "keno.....",
        "Emon kore na 😙",
        "No...",
        "Plssss",
        "Come on!",
        "Think again 😉",
        "Don't you want to? 🥺",
        "🤪 NE NE NE NE NE 🤪",
        "Beddop",
        "Pocha 🙂‍↔️",
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

        // 2. Move Button within viewport (especially important for mobile)
        if (container) {
            const rect = container.getBoundingClientRect();
            const viewportWidth = window.innerWidth;
            const viewportHeight = window.innerHeight;

            const btnWidth = 100; // Approximate button width
            const btnHeight = 50; // Approximate button height

            // Ensure button stays within viewport bounds
            const maxX = viewportWidth - btnWidth - 20; // 20px margin
            const maxY = viewportHeight - btnHeight - 20; // 20px margin

            // Get container position relative to viewport
            const containerLeft = rect.left;
            const containerTop = rect.top;

            // Calculate random position within viewport, preferring container area
            const randomX = Math.max(20, Math.min(maxX, containerLeft + Math.random() * Math.min(rect.width - btnWidth, maxX - containerLeft)));
            const randomY = Math.max(20, Math.min(maxY, containerTop + Math.random() * Math.min(rect.height - btnHeight, maxY - containerTop)));

            noBtnPosition = { left: `${randomX}px`, top: `${randomY}px` };
            isNoBtnMoved = true;
        }
    }
</script>

<main>
    <div class="container" bind:this={container}>
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
                        style:z-index={isNoBtnMoved ? "1000" : "auto"}
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
        transform: scale(1.5);
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

    /* Mobile responsiveness */
    @media (max-width: 768px) {
        .container {
            padding: 20px;
            max-width: 95%;
        }

        h1 {
            font-size: 2rem;
        }

        .buttons {
            flex-direction: column;
            gap: 15px;
        }

        button {
            padding: 12px 24px;
            font-size: 1rem;
        }
    }
</style>

