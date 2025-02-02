<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cakeroll's Journal</title>
    <link href="https://fonts.googleapis.com/css2?family=Lexend+Deca&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Lexend Deca', sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(to bottom right, #f7cac9, #92a8d1); /* Rose Quartz and Serenity */
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            color: #fff;
            flex-direction: column;
            text-align: center;
            overflow-x: hidden;
        }
        .login-container {
            width: 100%;
            max-width: 400px;
            background: rgba(0, 0, 0, 0.8);
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 8px 15px rgba(0, 0, 0, 0.5);
            text-align: center;
            margin: 0 auto;
        }
        h1 {
            font-size: 2.5rem;
            color: #ff66b3;
            margin-bottom: 20px;
        }
        h2 {
            color: #fff;
            margin-bottom: 20px;
        }
        input, button {
            width: 100%;
            padding: 12px;
            margin: 10px 0;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            background: rgba(255, 255, 255, 0.3);
            color: #fff;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
        }
        input:focus, button:focus {
            outline: none;
            box-shadow: 0 0 10px rgba(255, 102, 153, 0.8);
        }
        button {
            background: #ff66b3;
            color: white;
            cursor: pointer;
        }
        button:hover {
            background: #ff3399;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        .container {
            width: 100%;
            max-width: 1200px;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            background: rgba(0, 0, 0, 0.8);
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
            display: none;
            gap: 20px;
            flex-direction: row;
            overflow: hidden;
        }
        .entries, .entry-form {
            background: rgba(255, 255, 255, 0.1);
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            overflow: auto;
        }
        .entries {
            width: 45%;
            height: 500px;
            overflow-y: auto;
        }
        .entry-form {
            width: 45%;
            height: auto;
            overflow-y: hidden;
        }
        .entry {
            background: #ffccff;
            padding: 15px;
            margin: 10px 0;
            border-radius: 10px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            text-align: left;
            font-size: 12px;
        }
        .entry strong {
            display: block;
            color: #ff66b3;
            margin-bottom: 5px;
        }
        textarea {
            width: 100%;
            min-height: 200px;
            padding: 15px;
            border: 2px solid #ff66b3;
            border-radius: 10px;
            resize: none;
            font-size: 18px;
            background: rgba(255, 255, 255, 0.3);
            color: #fff;
            margin-top: 20px;
            overflow: hidden;
            box-sizing: border-box;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
        }
        .image-upload {
            margin-top: 15px;
            width: 100%; /* Align the file upload button with other elements */
        }
        .image-upload input {
            background: #ff66b3;
            color: white;
            border-radius: 10px;
            padding: 12px;
            font-size: 14px;
            border: none;
            width: 100%; /* Ensure the file input button width matches the other inputs */
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
            cursor: pointer;
            box-sizing: border-box; /* Prevent overflow */
        }
        .image-upload input:hover {
            background: #ff3399;
        }
        .entry-image {
            width: 100%;
            margin-top: 10px;
            border-radius: 10px;
        }
        .header-text {
            font-size: 24px;
            color: #ff66b3;
            margin-top: 20px;
            text-align: center;
        }
        /* New alignment styles */
        .login-container input, .login-container button, .login-container .show-password-btn {
            width: 100%;
            max-width: 350px; /* Adjusted max-width for better balance */
            margin: 10px auto;
        }
        .login-container .show-password-btn {
            background: #ff66b3;
            color: white;
            cursor: pointer;
            padding: 12px;
            margin: 10px 0;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
            border: none;
        }
        .login-container .show-password-btn:hover {
            background: #ff3399;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
    </style>
</head>
<body>
    <!-- Login Page -->
    <div class="login-container">
        <h1>Cakeroll's Journal</h1>
        <h2>Enter Password</h2>
        <input type="password" id="passwordInput" placeholder="Enter your password">
        <button onclick="checkPassword()">Login</button>
        <button class="show-password-btn" onclick="togglePassword()">Show Password</button>
    </div>

    <!-- Journal Page (hidden until login) -->
    <div class="container" id="journalContainer">
        <div class="entry-form">
            <h2>What's up Cakeroll</h2>
            <textarea id="journalEntry" placeholder="Write your thoughts here..."></textarea>
            <div class="image-upload">
                <input type="file" id="imageUpload" accept="image/*">
            </div>
            <button id="saveButton" onclick="saveEntry()">Save Entry</button>
        </div>
        <div class="entries" id="entriesList">
            <h1>Cakeroll's Journal</h1>
            <!-- Past entries will show up here -->
        </div>
    </div>

    <script>
        const correctPassword = "0613";
        let uploadedImage = null;

        function checkPassword() {
            let inputPassword = document.getElementById("passwordInput").value;
            if (inputPassword === correctPassword) {
                document.querySelector(".login-container").style.display = "none";
                document.getElementById("journalContainer").style.display = "flex";
            } else {
                alert("Incorrect password!");
            }
        }

        function togglePassword() {
            let passwordField = document.getElementById("passwordInput");
            if (passwordField.type === "password") {
                passwordField.type = "text";
            } else {
                passwordField.type = "password";
            }
        }

        function saveEntry() {
            let entry = document.getElementById("journalEntry").value;
            if (entry.trim() === "") {
                alert("Please write something before saving.");
                return;
            }
            let saveButton = document.getElementById("saveButton");
            saveButton.disabled = true;  // Disable save button to prevent multiple clicks
            let entries = JSON.parse(localStorage.getItem("journalEntries")) || [];
            let timestamp = new Date().toLocaleString();
            let imageUrl = uploadedImage ? uploadedImage : null;
            entries.push({ text: entry, date: timestamp, imageUrl: imageUrl });
            localStorage.setItem("journalEntries", JSON.stringify(entries));
            document.getElementById("journalEntry").value = "";
            document.getElementById("imageUpload").value = ""; // Reset the image input
            uploadedImage = null;
            displayEntries();
            alert("Journal entry saved!");
            saveButton.disabled = false;  // Re-enable save button
        }

        function displayEntries() {
            let entries = JSON.parse(localStorage.getItem("journalEntries")) || [];
            let entriesList = document.getElementById("entriesList");
            entriesList.innerHTML = "<h1>Cakeroll's Journal</h1>";
            entries.reverse(); // Reverse the order so the most recent entry is first
            entries.forEach((entry) => {
                let entryHtml = `<div class='entry'>
                    <strong>${entry.date}</strong>
                    <p>${entry.text}</p>`;
                if (entry.imageUrl) {
                    entryHtml += `<img src="${entry.imageUrl}" alt="Entry Image" class="entry-image">`;
                }
                entryHtml += `</div>`;
                entriesList.innerHTML += entryHtml;
            });
        }

        // Handle image upload
        document.getElementById("imageUpload").addEventListener('change', function(event) {
            let file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    uploadedImage = e.target.result;
                };
                reader.readAsDataURL(file);
            }
        });

        window.onload = displayEntries;
    </script>
</body>
</html>
