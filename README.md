
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>The Target – Embed Submission</title>
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
            width: 360px;
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
        const imageFile = form.image.files[0];

        const embed = {
            title: "🎯 The Target",
            color: 0xff0000,
            fields: [
                { name: "Roleplay Name", value: form.roleplayName.value, inline: true },
                { name: "Roblox Username", value: form.robloxUsername.value, inline: true },
                { name: "Occupation", value: form.occupation.value, inline: true },
                { name: "Vehicle", value: form.vehicle.value, inline: true },
                { name: "Registration", value: form.registration.value, inline: true },
                { name: "Reason", value: form.reason.value, inline: false }
            ],
            image: {
                url: "attachment://target-image.png"
            },
            footer: {
                text: "Target Submission System"
            },
            timestamp: new Date().toISOString()
        };

        const payload = {
            embeds: [embed]
        };

        const formData = new FormData();
        formData.append("payload_json", JSON.stringify(payload));
        formData.append("files[0]", imageFile, "target-image.png");

        try {
            const response = await fetch(webhookURL, {
                method: "POST",
                body: formData
            });

            if (response.ok) {
                alert("Embed sent successfully!");
                form.reset();
            } else {
                alert("Failed to send embed.");
            }
        } catch (error) {
            console.error(error);
            alert("Error sending embed.");
        }
    });
</script>

</body>
</html>
