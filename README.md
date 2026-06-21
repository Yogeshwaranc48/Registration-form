<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Client-Side Form Validation</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 400px;
            margin: 50px auto;
        }
        input {
            width: 100%;
            padding: 8px;
            margin: 5px 0;
        }
        .error {
            color: red;
            font-size: 14px;
            display: block;
            margin-bottom: 10px;
        }
        button {
            padding: 10px 15px;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <h2>Registration Form</h2>

    <form id="registrationForm">
        <input type="text" id="name" placeholder="Full Name">
        <span id="nameError" class="error"></span>

        <input type="email" id="email" placeholder="Email">
        <span id="emailError" class="error"></span>

        <input type="password" id="password" placeholder="Password">
        <span id="passwordError" class="error"></span>

        <input type="password" id="confirmPassword" placeholder="Confirm Password">
        <span id="confirmPasswordError" class="error"></span>

        <button type="submit">Submit</button>
    </form>

    <script>
        document.getElementById("registrationForm").addEventListener("submit", function(event) {
            event.preventDefault();

            let isValid = true;

            const name = document.getElementById("name").value.trim();
            const email = document.getElementById("email").value.trim();
            const password = document.getElementById("password").value;
            const confirmPassword = document.getElementById("confirmPassword").value;

            document.getElementById("nameError").textContent = "";
            document.getElementById("emailError").textContent = "";
            document.getElementById("passwordError").textContent = "";
            document.getElementById("confirmPasswordError").textContent = "";

            if (name === "") {
                document.getElementById("nameError").textContent = "Name is required";
                isValid = false;
            }

            const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            if (!emailPattern.test(email)) {
                document.getElementById("emailError").textContent = "Enter a valid email";
                isValid = false;
            }

            const passwordPattern =
                /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&]).{8,}$/;

            if (!passwordPattern.test(password)) {
                document.getElementById("passwordError").textContent =
                    "Password must be 8+ chars with uppercase, lowercase, number, and special character";
                isValid = false;
            }

            if (password !== confirmPassword) {
                document.getElementById("confirmPasswordError").textContent =
                    "Passwords do not match";
                isValid = false;
            }

            if (isValid) {
                alert("Form submitted successfully!");
            }
        });
    </script>

</body>
</html>
