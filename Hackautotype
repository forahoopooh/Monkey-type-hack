(async () => {
    const targetWPM = 300; // 🎯 Set speed here
    const msPerChar = 60000 / (targetWPM * 5);
    const input = document.querySelector("#wordsInput");

    console.log("BOT ATTEMPTING START...");

    async function startBot() {
        // 1. Force the cursor into the box
        input.focus();
        
        while (true) {
            // Find the word that the game wants you to type RIGHT NOW
            const activeWord = document.querySelector(".word.active");
            
            if (!activeWord) {
                // If there's no active word, the test is either not started or finished
                await new Promise(r => setTimeout(r, 250));
                continue;
            }

            // Get every letter in that specific word
            const letters = activeWord.querySelectorAll("letter");
            for (let i = 0; i < letters.length; i++) {
                const char = letters[i].innerText;
                
                // Inject character
                input.value += char;
                input.dispatchEvent(new InputEvent("input", { inputType: "insertText", data: char, bubbles: true }));
                
                await new Promise(r => setTimeout(r, msPerChar));
            }

            // Send Space to move to next word
            input.value += " ";
            input.dispatchEvent(new InputEvent("input", { inputType: "insertText", data: " ", bubbles: true }));
            input.dispatchEvent(new KeyboardEvent("keydown", { key: " ", code: "Space", keyCode: 32, bubbles: true }));
            
            // Tiny pause so it doesn't look like a glitch
            await new Promise(r => setTimeout(r, 10));
        }
    }

    startBot();
})();
