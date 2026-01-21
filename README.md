
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>The Target Submission</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #1e1e1e;
            color: #ffffff;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        form {
            background-color: #2b2b2b;
            padding: 20px;
            border-radius: 8px;
            width: 350px;
        }

        h2 {
            text-align: center;
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-top: 10px;
            font-size: 14px;
        }

        input, textarea, button {
            width: 100%;
            margin-top: 5px;
            padding: 8px;
            border-radius: 4px;
            border: none;
            font-size: 14px;
        }

        textarea {
            resize: vertical;
        }

        button {
            margin-top: 15px;
            background-color: #5865F2;
            color: white;
            cursor: pointer;
        }

        button:hover {
            background-color: #4752c4;
        }
    </style>
</head>
<body>

<form id="targetForm">
    <h2>The Target</h2>

    <label>Roleplay Name:</label>
    <input type="text" name="roleplayName" required>

    <label>Roblox Username:</label>
    <input type="text" name="robloxUsername" required>

    <label>Occupation:</label>
    <input type="text" name="occupation" required>

    <label>Vehicle:</label>
    <input type="text" name="vehicle" required>

    <label>Registration:</label>
    <input type="text" name="registration" required>

    <label>Reason:</label>
    <textarea name="reason" rows="3" required></textarea>

    <label>Image of Them:</label>
    <input type="file" name="image" accept="image/*" required>

    <button type="submit">Submit</button>
</form>

<script>
    const webhookURL = "https://discord.com/api/webhooks/1463449359327957129/1uDHBivWD8IKhlz8IbyyupXKMmTysCi-TS_9fD6NEnjmv5qzjb9eejp-KHSESine7Y5o";

    document.getElementById("targetForm").addEventListener("submit", async function (e) {
        e.preventDefault();

        const form = e.target;
        const formData = new FormData();

        const content =
`**🎯 The Target**
**Roleplay Name:** ${form.roleplayName.value}
**Roblox Username:** ${form.robloxUsername.value}
**Occupation:** ${form.occupation.value}
**Vehicle:** ${form.vehicle.value}
**Registration:** ${form.registration.value}
**Reason:** ${form.reason.value}`;

        formData.append("content", content);

        if (form.image.files.length > 0) {
            formData.append("files[0]", form.image.files[0]);
        }

        try {
            const response = await fetch(webhookURL, {
                method: "POST",
                body: formData
            });

            if (response.ok) {
                alert("Submission sent successfully!");
                form.reset();
            } else {
                alert("Failed to send submission.");
            }
        } catch (error) {
            alert("Error sending submission.");
            console.error(error);
        }
    });
</script>

</body>
</html>
