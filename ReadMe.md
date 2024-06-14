# Advanced Random Password Generator

This web app generates secure random passwords based on user-selected criteria. It includes features to view or hide the generated password and copy it to the clipboard. Additionally, it provides links to test the password strength and visit the main site.

## Features

- Generate random passwords with special characters, alphanumeric characters, mixed case, or lowercase only.
- Toggle password visibility between hidden and visible states.
- Copy the generated password to the clipboard.
- Links to test password strength and visit the main site.

## Usage

1. Select the desired character type from the dropdown menu.
2. Enter the desired password length (default is 16).
3. Click the "Generate Password" button to generate a password.
4. Use the "See/Hide" button to toggle password visibility.
5. Click "Copy to Clipboard" to copy the generated password.
6. Use the provided links to test password strength or visit the main site.

## Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Random Password Generator</title>
    <link href="https://fonts.googleapis.com/css?family=Roboto:400,500&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background: #fafafa;
        }
        .container {
            text-align: center;
            padding: 40px;
            background-color: #fff;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            border-radius: 10px;
            max-width: 400px;
            width: 100%;
        }
        select, input[type=number] {
            padding: 15px;
            margin: 15px 0;
            width: calc(100% - 30px);
            border: 1px solid #ddd;
            border-radius: 5px;
            box-sizing: border-box;
            font-size: 16px;
        }
        button {
            padding: 15px 30px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            width: calc(100% - 60px);
            font-size: 16px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #0056b3;
        }
        #passwordDisplay {
            margin: 20px 0;
            padding: 15px;
            background-color: #f7f7f7;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-family: 'Courier New', Courier, monospace;
            color: #333;
            word-wrap: break-word;
            height: 50px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            box-sizing: border-box;
        }
    </style>
</head>

<body>
    <div class="container">
        <h2>Generate a Random Password</h2>
        <select id="charType">
            <option value="special" selected>Include Special Characters</option>
            <option value="alphanumeric">Uppercase, Lowercase Letters and Digits</option>
            <option value="mixedcase">Uppercase and Lowercase Letters</option>
            <option value="lowercase">Lowercase Letters Only</option>
        </select>
        <input type="number" id="passwordLength" inputmode="numeric" pattern="[0-9]*" placeholder="Enter desired length (default: 16)..." min="1" max="128" required>
        <button onclick="generatePassword()">Generate Password</button>
        <div id="passwordDisplay"></div>
        <button id="toggleVisibilityButton" onclick="togglePasswordVisibility()">See</button>
        <br><br>
        <button onclick="copyToClipboard()">Copy to Clipboard</button>
        <br><br>
        <button class="button" onclick="window.open('https://strength.passwords.thedavidglass.com', '_blank');">Test Your Password Strength</button>
        <br><br>
        <button class="button" onclick="window.open('https://thedavidglass.com', '_blank');">Visit My Main Site</button>
    </div>
    
    <script>
        let isPasswordVisible = false;

        function generatePassword() {
            const charType = document.getElementById('charType').value;
            const length = parseInt(document.getElementById('passwordLength').value) || 16;
            const charsetLowercase = 'abcdefghijklmnopqrstuvwxyz';
            const charsetUppercase = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
            const charsetDigits = '0123456789';
            const charsetSpecial = '!@#$%^&*-_+=?~';
            let charset = '';

            switch(charType) {
                case 'lowercase':
                    charset = charsetLowercase;
                    break;
                case 'mixedcase':
                    charset = charsetLowercase + charsetUppercase;
                    break;
                case 'alphanumeric':
                    charset = charsetLowercase + charsetUppercase + charsetDigits;
                    break;
                case 'special':
                    charset = charsetLowercase + charsetUppercase + charsetDigits + charsetSpecial;
                    break;
                default:
                    charset = charsetLowercase + charsetUppercase + charsetDigits + charsetSpecial;
            }

            let password = '';
            for (let i = 0; i < length; i++) {
                password += charset.charAt(Math.floor(Math.random() * charset.length));
            }

            document.getElementById('passwordDisplay').dataset.originalText = password;
            updatePasswordVisibility();
        }

        function copyToClipboard() {
            const password = document.getElementById('passwordDisplay').dataset.originalText;
            navigator.clipboard.writeText(password).then(() => {
            }, (err) => {
                console.error('Error copying text to clipboard:', err);
                alert('Failed to copy password');
            });
        }

        function togglePasswordVisibility() {
            isPasswordVisible = !isPasswordVisible;
            updatePasswordVisibility();
        }

        function updatePasswordVisibility() {
            const passwordDisplay = document.getElementById('passwordDisplay');
            const visibilityButton = document.getElementById('toggleVisibilityButton');
            const originalText = passwordDisplay.dataset.originalText;

            if (isPasswordVisible) {
                passwordDisplay.innerText = originalText;
                visibilityButton.innerText = 'Hide';
            } else {
                passwordDisplay.innerText = '*'.repeat(originalText.length);
                visibilityButton.innerText = 'See';
            }
        }
    </script>
</body>
</html>
```
