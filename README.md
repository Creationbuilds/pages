<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ninja Notes - Login</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap');
        
        :root {
            --primary-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            --secondary-gradient: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            --success-gradient: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            --warning-gradient: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);
            --dark-bg: #0a0a0a;
            --card-bg: rgba(255, 255, 255, 0.05);
            --glass-bg: rgba(255, 255, 255, 0.1);
            --text-primary: #ffffff;
            --text-secondary: #a0a0a0;
            --border-color: rgba(255, 255, 255, 0.1);
            --shadow-primary: 0 8px 32px rgba(0, 0, 0, 0.3);
            --shadow-hover: 0 12px 40px rgba(0, 0, 0, 0.4);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', sans-serif;
            background: var(--dark-bg);
            color: var(--text-primary);
            overflow-x: hidden;
            line-height: 1.6;
            min-height: 100vh;
        }

        /* Background Animation */
        .bg-animation {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0.1;
        }

        .bg-animation::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at 20% 80%, #667eea 0%, transparent 50%),
                       radial-gradient(circle at 80% 20%, #764ba2 0%, transparent 50%),
                       radial-gradient(circle at 40% 40%, #f093fb 0%, transparent 50%);
            animation: backgroundShift 15s ease-in-out infinite;
        }

        @keyframes backgroundShift {
            0%, 100% { transform: scale(1) rotate(0deg); }
            50% { transform: scale(1.1) rotate(180deg); }
        }

        /* Navbar */
        .navbar {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            background: rgba(10, 10, 10, 0.9);
            backdrop-filter: blur(20px);
            border-bottom: 1px solid var(--border-color);
            z-index: 1000;
            padding: 1rem 0;
        }

        .nav-container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 0 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: 800;
            background: var(--primary-gradient);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-decoration: none;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .logo i {
            background: var(--primary-gradient);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        .back-btn {
            color: var(--text-secondary);
            text-decoration: none;
            font-weight: 500;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            padding: 0.5rem 1rem;
            border-radius: 0.5rem;
            border: 1px solid var(--border-color);
        }

        .back-btn:hover {
            color: var(--text-primary);
            background: var(--glass-bg);
            transform: translateX(-2px);
        }

        /* Main Container */
        .main-container {
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            padding: 2rem;
            margin-top: 80px;
        }

        /* Auth Container */
        .auth-container {
            background: var(--card-bg);
            backdrop-filter: blur(20px);
            border: 1px solid var(--border-color);
            border-radius: 2rem;
            padding: 3rem;
            max-width: 450px;
            width: 100%;
            box-shadow: var(--shadow-primary);
            position: relative;
            overflow: hidden;
            animation: slideInUp 0.8s ease-out;
        }

        @keyframes slideInUp {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .auth-container::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: var(--primary-gradient);
        }

        .auth-header {
            text-align: center;
            margin-bottom: 2rem;
        }

        .auth-header h1 {
            font-size: 2.5rem;
            font-weight: 800;
            margin-bottom: 0.5rem;
            background: var(--primary-gradient);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .auth-header p {
            color: var(--text-secondary);
            font-size: 1.1rem;
        }

        /* Form Styles */
        .auth-form {
            display: block;
        }

        .auth-form.hidden {
            display: none;
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
            color: var(--text-primary);
        }

        .form-group input {
            width: 100%;
            padding: 1rem;
            background: var(--glass-bg);
            border: 2px solid var(--border-color);
            border-radius: 0.75rem;
            color: var(--text-primary);
            font-size: 1rem;
            transition: all 0.3s ease;
        }

        .form-group input:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
            transform: translateY(-2px);
        }

        .form-group input::placeholder {
            color: var(--text-secondary);
        }

        /* OTP Input Style */
        .otp-container {
            display: flex;
            gap: 1rem;
            justify-content: center;
            margin: 2rem 0;
        }

        .otp-input {
            width: 60px;
            height: 60px;
            text-align: center;
            font-size: 1.5rem;
            font-weight: 700;
            border: 2px solid var(--border-color);
            border-radius: 0.75rem;
            background: var(--glass-bg);
            color: var(--text-primary);
            transition: all 0.3s ease;
        }

        .otp-input:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
            transform: scale(1.05);
        }

        .otp-input.filled {
            border-color: #4facfe;
            background: rgba(79, 172, 254, 0.1);
        }

        /* Button Styles */
        .btn {
            padding: 1rem 2rem;
            border: none;
            border-radius: 0.75rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            font-size: 1rem;
            position: relative;
            overflow: hidden;
            width: 100%;
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
            transition: left 0.5s;
        }

        .btn:hover::before {
            left: 100%;
        }

        .btn-primary {
            background: var(--primary-gradient);
            color: white;
            box-shadow: 0 4px 20px rgba(102, 126, 234, 0.4);
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 30px rgba(102, 126, 234, 0.6);
        }

        .btn-primary:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .btn-secondary {
            background: transparent;
            color: var(--text-primary);
            border: 2px solid var(--border-color);
        }

        .btn-secondary:hover {
            background: var(--glass-bg);
            border-color: rgba(255, 255, 255, 0.3);
        }

        .btn-success {
            background: var(--success-gradient);
            color: white;
            box-shadow: 0 4px 20px rgba(79, 172, 254, 0.4);
        }

        .btn-success:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 30px rgba(79, 172, 254, 0.6);
        }

        /* Timer and Resend */
        .timer-container {
            text-align: center;
            margin: 1rem 0;
        }

        .timer {
            font-size: 1.2rem;
            font-weight: 600;
            color: #4facfe;
            margin-bottom: 0.5rem;
        }

        .resend-btn {
            color: var(--text-secondary);
            background: none;
            border: none;
            cursor: pointer;
            font-size: 0.9rem;
            text-decoration: underline;
            transition: color 0.3s ease;
        }

        .resend-btn:hover {
            color: var(--text-primary);
        }

        .resend-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        /* Success Animation */
        .success-animation {
            text-align: center;
            margin: 2rem 0;
        }

        .success-icon {
            font-size: 4rem;
            color: #4facfe;
            margin-bottom: 1rem;
            animation: bounce 0.8s ease-in-out;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-30px); }
            60% { transform: translateY(-15px); }
        }

        /* Profile Section */
        .profile-section {
            display: none;
            text-align: center;
            padding: 2rem 0;
        }

        .profile-section.active {
            display: block;
        }

        .profile-avatar {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            background: var(--primary-gradient);
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 1rem;
            font-size: 3rem;
            color: white;
            font-weight: 700;
            box-shadow: 0 8px 30px rgba(102, 126, 234, 0.4);
        }

        .profile-name {
            font-size: 1.8rem;
            font-weight: 700;
            margin-bottom: 0.5rem;
            color: var(--text-primary);
        }

        .profile-email {
            color: var(--text-secondary);
            margin-bottom: 2rem;
        }

        .profile-stats {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 1rem;
            margin: 2rem 0;
        }

        .stat-item {
            background: var(--glass-bg);
            padding: 1rem;
            border-radius: 0.75rem;
            border: 1px solid var(--border-color);
            text-align: center;
        }

        .stat-value {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--text-primary);
        }

        .stat-label {
            color: var(--text-secondary);
            font-size: 0.9rem;
        }

        /* Notification */
        .notification {
            position: fixed;
            top: 6rem;
            right: 2rem;
            padding: 1rem 1.5rem;
            border-radius: 0.75rem;
            color: white;
            font-weight: 600;
            z-index: 3000;
            transform: translateX(400px);
            transition: transform 0.3s ease;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .notification.show {
            transform: translateX(0);
        }

        .notification.success {
            background: var(--success-gradient);
        }

        .notification.error {
            background: var(--secondary-gradient);
        }

        .notification.warning {
            background: var(--warning-gradient);
        }

        /* Loading Spinner */
        .loading-spinner {
            width: 20px;
            height: 20px;
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-top: 2px solid white;
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .nav-container {
                padding: 0 1rem;
            }

            .auth-container {
                padding: 2rem;
                margin: 1rem;
            }

            .auth-header h1 {
                font-size: 2rem;
            }

            .otp-container {
                gap: 0.5rem;
            }

            .otp-input {
                width: 50px;
                height: 50px;
                font-size: 1.2rem;
            }

            .profile-stats {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 480px) {
            .main-container {
                padding: 1rem;
            }

            .auth-container {
                padding: 1.5rem;
            }

            .otp-input {
                width: 45px;
                height: 45px;
                font-size: 1rem;
            }
        }
    </style>
</head>
<body>
    <div class="bg-animation"></div>
    
    <!-- Navigation -->
    <nav class="navbar">
        <div class="nav-container">
            <a href="#" class="logo">
                <i class="fas fa-user-ninja"></i>
                Ninja Notes
            </a>
            
            <a href="#" class="back-btn" onclick="goToHome()">
                <i class="fas fa-arrow-left"></i>
                Back to Home
            </a>
        </div>
    </nav>

    <!-- Main Container -->
    <div class="main-container">
        <div class="auth-container">
            <!-- Email Form -->
            <div class="auth-form" id="emailForm">
                <div class="auth-header">
                    <h1><i class="fas fa-sign-in-alt"></i></h1>
                    <h1>Welcome Back</h1>
                    <p>Enter your email to continue</p>
                </div>
                
                <form id="loginForm" onsubmit="sendOTP(event)">
                    <div class="form-group">
                        <label for="email">Email Address</label>
                        <input type="email" id="email" required placeholder="Enter your email address">
                    </div>
                    
                    <button type="submit" class="btn btn-primary" id="sendOtpBtn">
                        <i class="fas fa-paper-plane"></i>
                        Send OTP
                    </button>
                </form>
            </div>

            <!-- OTP Verification Form -->
            <div class="auth-form hidden" id="otpForm">
                <div class="auth-header">
                    <h1><i class="fas fa-shield-alt"></i></h1>
                    <h1>Verify OTP</h1>
                    <p>Enter the 6-digit code sent to your email</p>
                </div>
                
                <form id="verifyForm" onsubmit="verifyOTP(event)">
                    <div class="otp-container">
                        <input type="text" class="otp-input" maxlength="1" oninput="handleOTPInput(this, 0)">
                        <input type="text" class="otp-input" maxlength="1" oninput="handleOTPInput(this, 1)">
                        <input type="text" class="otp-input" maxlength="1" oninput="handleOTPInput(this, 2)">
                        <input type="text" class="otp-input" maxlength="1" oninput="handleOTPInput(this, 3)">
                        <input type="text" class="otp-input" maxlength="1" oninput="handleOTPInput(this, 4)">
                        <input type="text" class="otp-input" maxlength="1" oninput="handleOTPInput(this, 5)">
                    </div>
                    
                    <div class="timer-container">
                        <div class="timer" id="timer">02:00</div>
                        <button type="button" class="resend-btn" id="resendBtn" onclick="resendOTP()" disabled>
                            Resend OTP
                        </button>
                    </div>
                    
                    <button type="submit" class="btn btn-success" id="verifyBtn">
                        <i class="fas fa-check"></i>
                        Verify & Login
                    </button>
                </form>
                
                <button type="button" class="btn btn-secondary" onclick="goBack()" style="margin-top: 1rem;">
                    <i class="fas fa-arrow-left"></i>
                    Back to Email
                </button>
            </div>

            <!-- Success Screen -->
            <div class="auth-form hidden" id="successForm">
                <div class="success-animation">
                    <div class="success-icon">
                        <i class="fas fa-check-circle"></i>
                    </div>
                    <h2>Login Successful!</h2>
                    <p>Redirecting to your dashboard...</p>
                </div>
            </div>

            <!-- Profile Section -->
            <div class="profile-section" id="profileSection">
                <div class="profile-avatar" id="profileAvatar">
                    JD
                </div>
                <div class="profile-name" id="profileName">John Doe</div>
                <div class="profile-email" id="profileEmail">john.doe@example.com</div>
                
                <div class="profile-stats">
                    <div class="stat-item">
                        <div class="stat-value">12</div>
                        <div class="stat-label">Notes Purchased</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value">5</div>
                        <div class="stat-label">Notes Sold</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value">4.8</div>
                        <div class="stat-label">Rating</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value">₹2,450</div>
                        <div class="stat-label">Earnings</div>
                    </div>
                </div>
                
                <button class="btn btn-primary" onclick="goToHome()">
                    <i class="fas fa-home"></i>
                    Go to Home
                </button>
            </div>
        </div>
    </div>

    <!-- Notification -->
    <div class="notification" id="notification">
        <i class="fas fa-info-circle"></i>
        <span id="notificationText"></span>
    </div>

    <script>
        // State management
        let currentStep = 'email';
        let timer = null;
        let timeLeft = 120; // 2 minutes
        let userEmail = '';
        let generatedOTP = '';

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            // Focus on email input
            document.getElementById('email').focus();
            
            // Handle enter key for OTP inputs
            document.querySelectorAll('.otp-input').forEach(input => {
                input.addEventListener('keydown', function(e) {
                    if (e.key === 'Enter') {
                        e.preventDefault();
                        document.getElementById('verifyForm').dispatchEvent(new Event('submit'));
                    }
                });
            });
        });

        // Send OTP
        function sendOTP(event) {
            event.preventDefault();
            
            const email = document.getElementById('email').value;
            const sendOtpBtn = document.getElementById('sendOtpBtn');
            
            if (!email) {
                showNotification('Please enter your email address', 'error');
                return;
            }
            
            // Show loading
            sendOtpBtn.innerHTML = '<div class="loading-spinner"></div> Sending OTP...';
            sendOtpBtn.disabled = true;
            
            // Simulate API call
            setTimeout(() => {
                userEmail = email;
                generatedOTP = Math.floor(100000 + Math.random() * 900000).toString();
                
                // Log OTP to console for demo (in real app, this would be sent via email)
                console.log('Generated OTP:', generatedOTP);
                
                showNotification(`OTP sent to ${email}. Check console for demo OTP: ${generatedOTP}`, 'success');
                
                // Switch to OTP form
                switchToOTPForm();
                
                // Reset button
                sendOtpBtn.innerHTML = '<i class="fas fa-paper-plane"></i> Send OTP';
                sendOtpBtn.disabled = false;
            }, 2000);
        }

        // Switch to OTP form
        function switchToOTPForm() {
            document.getElementById('emailForm').classList.add('hidden');
            document.getElementById('otpForm').classList.remove('hidden');
            
            // Focus on first OTP input
            document.querySelector('.otp-input').focus();
            
            // Start timer
            startTimer();
            
            currentStep = 'otp';
        }

        // Handle OTP input
        function handleOTPInput(input, index) {
            const value = input.value;
            
            // Only allow numbers
            if (!/^\d*$/.test(value)) {
                input.value = '';
                return;
            }
            
            // Add filled class
            if (value) {
                input.classList.add('filled');
            } else {
                input.classList.remove('filled');
            }
            
            // Auto-focus next input
            if (value && index < 5) {
                const nextInput = document.querySelectorAll('.otp-input')[index + 1];
                nextInput.focus();
            }
            
            // Auto-submit when all fields are filled
            const allInputs = document.querySelectorAll('.otp-input');
            const allFilled = Array.from(allInputs).every(inp => inp.value);
            
            if (allFilled) {
                setTimeout(() => {
                    document.getElementById('verifyForm').dispatchEvent(new Event('submit'));
                }, 500);
            }
        }

        // Verify OTP
        function verifyOTP(event) {
            event.preventDefault();
            
            const otpInputs = document.querySelectorAll('.otp-input');
            const enteredOTP = Array.from(otpInputs).map(input => input.value).join('');
            const verifyBtn = document.getElementById('verifyBtn');
            
            if (enteredOTP.length !== 6) {
                showNotification('Please enter complete OTP', 'error');
                return;
            }
            
            // Show loading
            verifyBtn.innerHTML = '<div class="loading-spinner"></div> Verifying...';
            verifyBtn.disabled = true;
            
            // Simulate API call
            setTimeout(() => {
                if (enteredOTP === generatedOTP) {
                    // Success
                    clearInterval(timer);
                    showNotification('OTP verified successfully!', 'success');
                    
                    // Switch to success screen
                    switchToSuccessScreen();
                } else {
                    // Error
                    showNotification('Invalid OTP. Please try again.', 'error');
                    
                    // Clear inputs and focus first
                    otpInputs.forEach(input => {
                        input.value = '';
                        input.classList.remove('filled');
                    });
                    otpInputs[0].focus();
                }
                
                // Reset button
                verifyBtn.innerHTML = '<i class="fas fa-check"></i> Verify & Login';
                verifyBtn.disabled = false;
            }, 2000);
        }

        // Switch to success screen
        function switchToSuccessScreen() {
            document.getElementById('otpForm').classList.add('hidden');
            document.getElementById('successForm').classList.remove('hidden');
            
            // Redirect after 3 seconds
            setTimeout(() => {
                showProfile();
            }, 3000);
        }

        // Show profile
        function showProfile() {
            document.getElementById('successForm').classList.add('hidden');
            document.getElementById('profileSection').classList.add('active');
            
            // Update profile with user data
            const name = userEmail.split('@')[0];
            const initials = name.split('.').map(part => part[0].toUpperCase()).join('');
            
            document.getElementById('profileAvatar').textContent = initials;
            document.getElementById('profileName').textContent = name.replace('.', ' ').replace(/\b\w/g, l => l.toUpperCase());
            document.getElementById('profileEmail').textContent = userEmail;
        }

        // Start timer
        function startTimer() {
            timeLeft = 120;
            document.getElementById('resendBtn').disabled = true;
            
            timer = setInterval(() => {
                timeLeft--;
                
                const minutes = Math.floor(timeLeft / 60);
                const seconds = timeLeft % 60;
                
                document.getElementById('timer').textContent = 
                    `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
                
                if (timeLeft === 0) {
                    clearInterval(timer);
                    document.getElementById('resendBtn').disabled = false;
                    document.getElementById('timer').textContent = 'OTP Expired';
                }
            }, 1000);
        }

        // Resend OTP
        function resendOTP() {
            const resendBtn = document.getElementById('resendBtn');
            
            resendBtn.innerHTML = '<div class="loading-spinner"></div> Sending...';
            resendBtn.disabled = true;
            
            setTimeout(() => {
                // Generate new OTP
                generatedOTP = Math.floor(100000 + Math.random() * 900000).toString();
                console.log('New OTP:', generatedOTP);
                
                showNotification(`New OTP sent! Check console: ${generatedOTP}`, 'success');
                
                // Reset timer
                startTimer();
                
                // Clear inputs
                document.querySelectorAll('.otp-input').forEach(input => {
                    input.value = '';
                    input.classList.remove('filled');
                });
                
                resendBtn.innerHTML = 'Resend OTP';
            }, 2000);
        }

        // Go back to email form
        function goBack() {
            if (timer) {
                clearInterval(timer);
            }
            
            document.getElementById('otpForm').classList.add('hidden');
            document.getElementById('emailForm').classList.remove('hidden');
            
            // Clear OTP inputs
            document.querySelectorAll('.otp-input').forEach(input => {
                input.value = '';
                input.classList.remove('filled');
            });
            
            // Focus on email input
            document.getElementById('email').focus();
            
            currentStep = 'email';
        }

        // Go to home page
        function goToHome() {
            // In a real app, this would redirect to the home page
