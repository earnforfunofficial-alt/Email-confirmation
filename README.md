<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Exclusive Reward Claim</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #6c5ce7;
            --secondary: #a29bfe;
            --accent: #fd79a8;
            --error: #ff7675;
            --dark: #2d3436;
            --light: #f5f6fa;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
        }

        body {
            background: linear-gradient(135deg, #1a1a2e, #16213e);
            color: var(--light);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
        }

        .particles {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .particle {
            position: absolute;
            background-color: rgba(255, 255, 255, 0.8);
            border-radius: 50%;
            animation: float var(--duration) infinite ease-in-out;
            opacity: var(--opacity);
        }

        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(180deg); }
        }

        .container {
            position: relative;
            z-index: 1;
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(15px);
            border-radius: 20px;
            padding: 40px;
            width: 100%;
            max-width: 500px;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.15);
            transform-style: preserve-3d;
            perspective: 1000px;
            overflow: hidden;
            transition: all 0.5s ease;
        }

        .container:hover {
            transform: translateY(-5px);
            box-shadow: 0 30px 60px -12px rgba(0, 0, 0, 0.4);
        }

        .logo {
            text-align: center;
            margin-bottom: 30px;
            animation: pulse 2s infinite;
        }

        .logo i {
            font-size: 60px;
            color: var(--accent);
            filter: drop-shadow(0 0 15px rgba(253, 121, 168, 0.5));
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }

        h1 {
            text-align: center;
            margin-bottom: 20px;
            font-weight: 700;
            font-size: 28px;
            background: linear-gradient(to right, var(--light), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 15px rgba(255, 255, 255, 0.2);
        }

        .subtitle {
            text-align: center;
            margin-bottom: 30px;
            color: rgba(255, 255, 255, 0.8);
            font-size: 16px;
            line-height: 1.6;
        }

        .form-group {
            margin-bottom: 25px;
            position: relative;
        }

        .form-group label {
            display: block;
            margin-bottom: 10px;
            font-weight: 600;
            color: var(--light);
            font-size: 14px;
        }

        .input-field {
            position: relative;
        }

        .input-field input {
            width: 100%;
            padding: 16px 20px;
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.2);
            border-radius: 12px;
            color: var(--light);
            font-size: 16px;
            transition: all 0.3s ease;
        }

        .input-field input:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 4px rgba(253, 121, 168, 0.2);
            background: rgba(255, 255, 255, 0.15);
        }

        .input-field input::placeholder {
            color: rgba(255, 255, 255, 0.5);
        }

        .error-message {
            color: var(--error);
            font-size: 13px;
            margin-top: 8px;
            display: none;
        }

        .btn {
            width: 100%;
            padding: 16px;
            background: linear-gradient(45deg, var(--primary), var(--accent));
            border: none;
            border-radius: 12px;
            color: var(--light);
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            z-index: 1;
            box-shadow: 0 10px 20px rgba(108, 92, 231, 0.3);
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(45deg, var(--accent), var(--primary));
            transition: all 0.4s ease;
            z-index: -1;
        }

        .btn:hover::before {
            left: 0;
        }

        .btn:disabled {
            background: rgba(255, 255, 255, 0.1);
            cursor: not-allowed;
        }

        .btn:disabled::before {
            display: none;
        }

        .btn i {
            margin-left: 8px;
            transition: transform 0.3s ease;
        }

        .btn:hover i {
            transform: translateX(5px);
        }

        .success-overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.9);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.5s ease;
        }

        .success-overlay.active {
            opacity: 1;
            pointer-events: all;
        }

        .success-content {
            text-align: center;
            max-width: 400px;
            padding: 0 20px;
        }

        .success-content i {
            font-size: 80px;
            color: var(--accent);
            margin-bottom: 20px;
            animation: bounce 0.5s;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }

        .success-content h2 {
            font-size: 28px;
            margin-bottom: 15px;
            color: var(--light);
        }

        .success-content p {
            color: rgba(255, 255, 255, 0.8);
            margin-bottom: 30px;
            line-height: 1.6;
        }

        .closed-message {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: #000;
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 2000;
            color: var(--light);
            font-size: 24px;
            text-align: center;
            padding: 20px;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.5s ease;
        }

        .closed-message.active {
            opacity: 1;
            pointer-events: all;
        }

        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: var(--accent);
            opacity: 0;
            z-index: 10;
        }

        .ripple {
            position: absolute;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.4);
            transform: scale(0);
            animation: ripple 0.6s linear;
            pointer-events: none;
        }

        @keyframes ripple {
            to {
                transform: scale(2.5);
                opacity: 0;
            }
        }

        @media (max-width: 600px) {
            .container {
                padding: 30px;
                margin: 20px;
            }
            
            h1 {
                font-size: 24px;
            }
        }
    </style>
</head>
<body>
    <div class="particles" id="particles"></div>

    <div class="container" id="mainContainer">
        <div class="logo">
            <i class="fas fa-gift"></i>
        </div>
        
        <h1>Claim Your Exclusive Reward</h1>
        <p class="subtitle">Enter your email below to confirm your eligibility. Only one submission allowed per email.</p>
        
        <form id="emailForm">
            <div class="form-group">
                <label for="email">Email Address</label>
                <div class="input-field">
                    <input type="email" id="email" placeholder="Enter email here" required>
                    <div class="error-message" id="emailError"></div>
                </div>
            </div>
            
            <button type="submit" class="btn" id="confirmBtn">
                Confirm Email <i class="fas fa-paper-plane"></i>
            </button>
        </form>
    </div>

    <div class="success-overlay" id="successOverlay">
        <div class="success-content">
            <i class="fas fa-check-circle"></i>
            <h2>Email Confirmed!</h2>
            <p>Your reward will be delivered to your email within 2 hours. Please check your inbox.</p>
            <button class="btn" id="closeSuccessBtn">
                <i class="fas fa-times"></i> Close
            </button>
        </div>
    </div>

    <div class="closed-message" id="closedMessage">
        <div>
            <i class="fas fa-lock" style="font-size: 50px; margin-bottom: 20px;"></i>
            <h2>Submission Closed</h2>
            <p>You've already confirmed your email. Please check your inbox for your reward.</p>
        </div>
    </div>

    <audio id="clickSound" src="https://assets.mixkit.co/sfx/preview/mixkit-modern-click-box-check-1120.mp3" preload="auto"></audio>
    <audio id="successSound" src="https://assets.mixkit.co/sfx/preview/mixkit-achievement-bell-600.mp3" preload="auto"></audio>
    <audio id="errorSound" src="https://assets.mixkit.co/sfx/preview/mixkit-warning-alarm-688.mp3" preload="auto"></audio>

    <script>
        // Create floating particles
        const particlesContainer = document.getElementById('particles');
        for (let i = 0; i < 50; i++) {
            const particle = document.createElement('div');
            particle.classList.add('particle');
            particle.style.left = `${Math.random() * 100}%`;
            particle.style.top = `${Math.random() * 100}%`;
            particle.style.width = `${Math.random() * 6 + 2}px`;
            particle.style.height = particle.style.width;
            particle.style.setProperty('--duration', `${Math.random() * 10 + 5}s`);
            particle.style.setProperty('--opacity', Math.random() * 0.6 + 0.2);
            particle.style.animationDelay = `${Math.random() * 5}s`;
            particlesContainer.appendChild(particle);
        }

        // DOM elements
        const emailForm = document.getElementById('emailForm');
        const emailInput = document.getElementById('email');
        const emailError = document.getElementById('emailError');
        const confirmBtn = document.getElementById('confirmBtn');
        const successOverlay = document.getElementById('successOverlay');
        const closeSuccessBtn = document.getElementById('closeSuccessBtn');
        const closedMessage = document.getElementById('closedMessage');
        const mainContainer = document.getElementById('mainContainer');
        
        // Audio elements
        const clickSound = document.getElementById('clickSound');
        const successSound = document.getElementById('successSound');
        const errorSound = document.getElementById('errorSound');
        
        // Track submitted emails
        const submittedEmails = new Set();
        
        // Ripple effect for buttons
        function createRipple(event) {
            const button = event.currentTarget;
            const circle = document.createElement('span');
            const diameter = Math.max(button.clientWidth, button.clientHeight);
            const radius = diameter / 2;
            
            circle.style.width = circle.style.height = `${diameter}px`;
            circle.style.left = `${event.clientX - button.getBoundingClientRect().left - radius}px`;
            circle.style.top = `${event.clientY - button.getBoundingClientRect().top - radius}px`;
            circle.classList.add('ripple');
            
            const ripple = button.getElementsByClassName('ripple')[0];
            if (ripple) {
                ripple.remove();
            }
            
            button.appendChild(circle);
        }

        // Add ripple to all buttons
        const buttons = document.querySelectorAll('button');
        buttons.forEach(button => {
            button.addEventListener('click', createRipple);
        });

        // Validate email format
        function isValidEmail(email) {
            // Only allow specific domains
            const allowedDomains = ['gmail.com', 'yahoo.com', 'outlook.com', 'hotmail.com'];
            const domain = email.split('@')[1];
            
            if (!domain) return false;
            
            return allowedDomains.some(allowed => 
                domain === allowed || domain.endsWith(`.${allowed}`)
            );
        }

        // Form submission
        emailForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            const email = emailInput.value.trim();
            
            // Play click sound
            playSound(clickSound);
            
            // Validate email
            if (!isValidEmail(email)) {
                emailError.textContent = "Please use a Gmail, Yahoo, or Outlook email address";
                emailError.style.display = 'block';
                playSound(errorSound);
                return;
            }
            
            // Check for duplicate email
            if (submittedEmails.has(email)) {
                emailError.textContent = "This email has already been submitted";
                emailError.style.display = 'block';
                playSound(errorSound);
                return;
            }
            
            // Hide error if valid
            emailError.style.display = 'none';
            
            // Disable form
            emailInput.disabled = true;
            confirmBtn.disabled = true;
            confirmBtn.innerHTML = '<i class="fas fa-check"></i> Confirmed';
            
            // Add to submitted emails
            submittedEmails.add(email);
            
            // Store in localStorage
            localStorage.setItem('submittedEmail', email);
            
            // Show success overlay
            setTimeout(() => {
                successOverlay.classList.add('active');
                createConfetti();
                playSound(successSound);
            }, 1000);
        });

        // Close success overlay
        closeSuccessBtn.addEventListener('click', function() {
            successOverlay.classList.remove('active');
            mainContainer.style.display = 'none';
            closedMessage.classList.add('active');
            playSound(clickSound);
        });

        // Play sound with error handling
        function playSound(sound) {
            sound.currentTime = 0;
            sound.play().catch(e => console.log("Sound playback prevented:", e));
        }

        // Confetti effect
        function createConfetti() {
            const colors = ['#6c5ce7', '#fd79a8', '#00cec9', '#fdcb6e', '#e17055', '#a29bfe'];
            
            for (let i = 0; i < 100; i++) {
                const confetti = document.createElement('div');
                confetti.classList.add('confetti');
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.left = `${Math.random() * 100}%`;
                confetti.style.top = '-10px';
                confetti.style.transform = `rotate(${Math.random() * 360}deg)`;
                confetti.style.width = `${Math.random() * 10 + 5}px`;
                confetti.style.height = `${Math.random() * 10 + 5}px`;
                confetti.style.borderRadius = Math.random() > 0.5 ? '50%' : '0';
                
                const animationDuration = Math.random() * 3 + 2;
                confetti.style.animation = `confettiFall ${animationDuration}s linear forwards`;
                
                document.body.appendChild(confetti);
                
                // Create keyframes for each confetti
                const keyframes = `
                    @keyframes confettiFall {
                        0% {
                            transform: translateY(0) rotate(0deg);
                            opacity: 1;
                        }
                        100% {
                            transform: translateY(100vh) rotate(${Math.random() * 360}deg);
                            opacity: 0;
                        }
                    }
                `;
                
                const style = document.createElement('style');
                style.innerHTML = keyframes;
                document.head.appendChild(style);
                
                // Remove confetti after animation
                setTimeout(() => {
                    confetti.remove();
                    style.remove();
                }, animationDuration * 1000);
            }
        }

        // Check for previously submitted email
        window.addEventListener('DOMContentLoaded', function() {
            const savedEmail = localStorage.getItem('submittedEmail');
            if (savedEmail) {
                mainContainer.style.display = 'none';
                closedMessage.classList.add('active');
            }
            
            // Enable audio on first interaction
            document.body.addEventListener('click', function initAudio() {
                // Play and immediately pause to unlock audio
                clickSound.play().then(() => {
                    clickSound.pause();
                    clickSound.currentTime = 0;
                }).catch(e => console.log(e));
                
                // Remove the event listener after first interaction
                document.body.removeEventListener('click', initAudio);
            }, { once: true });
        });
    </script>
</body>
</html>
