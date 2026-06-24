document.addEventListener('DOMContentLoaded', function() {
    const envelope = document.getElementById('envelope');
    const letterContainer = document.getElementById('letterContainer');
    const resetBtn = document.getElementById('resetBtn');
    const heartsContainer = document.getElementById('heartsContainer');

    // Open envelope on click
    envelope.addEventListener('click', function() {
        envelope.classList.add('open');
        letterContainer.classList.add('show');
        resetBtn.classList.add('show');
        
        // Create floating hearts
        createFloatingHearts();
    });

    // Reset to initial state
    resetBtn.addEventListener('click', function() {
        envelope.classList.remove('open');
        letterContainer.classList.remove('show');
        resetBtn.classList.remove('show');
        heartsContainer.innerHTML = '';
    });

    // Create floating hearts animation
    function createFloatingHearts() {
        const hearts = ['❤️', '💕', '💖', '💝', '💗', '💓', '💞'];
        
        for (let i = 0; i < 15; i++) {
            setTimeout(() => {
                const heart = document.createElement('div');
                heart.classList.add('heart');
                heart.textContent = hearts[Math.floor(Math.random() * hearts.length)];
                
                const startX = Math.random() * window.innerWidth;
                const duration = 3 + Math.random() * 2; // 3-5 seconds
                const delay = Math.random() * 0.5; // stagger the animation
                
                heart.style.left = startX + 'px';
                heart.style.bottom = '-30px';
                heart.style.animation = `float ${duration}s linear ${delay}s forwards`;
                
                heartsContainer.appendChild(heart);
                
                // Remove heart element after animation completes
                setTimeout(() => {
                    heart.remove();
                }, (duration + delay) * 1000);
            }, i * 100);
        }
    }

    // Add keyboard support - press 'o' to open, 'r' to reset
    document.addEventListener('keydown', function(event) {
        if (event.key.toLowerCase() === 'o' && !envelope.classList.contains('open')) {
            envelope.click();
        }
        if (event.key.toLowerCase() === 'r' && envelope.classList.contains('open')) {
            resetBtn.click();
        }
    });
});
