<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
    <title>Chat</title>
    <script src="https://cdn.jsdelivr.net/npm/comfy.js@latest/dist/comfy.min.js"></script>
    <style>
        html,
        body {
            margin-left: 10px;
            font-family: roboto;
            color: hsl(260, 72%, 12%);
        }

        #chat {
            width: 400px;
            height: 600px;
            overflow-y: auto;
            display: flex;
            flex-direction: column-reverse;
        }

        #chat::-webkit-scrollbar {
            display: none;
        }

        #chat ul {
            list-style-type: none;
            list-style-position: outside;
        }

        #chat li {
            background-color: hsl(262, 46%, 85%);
            box-sizing: border-box;
            padding: 1rem 10px;
            margin-bottom: 10px;
            margin-left: 10px;
            border: 0;
            border-radius: 50px;
        }

        #chat li.mod {
            padding: 10px;
            background-color: hsl(260, 20%, 89%);
            color: hsl(272, 90%, 28%);
          border-radius: 50px;
        }

        #chat li.sub {
            padding: 10px;
            background-color: hsl(230, 20%, 89%);
            color: hsl(242, 90%, 28%);
          border-radius: 50px;
        }

        #chat blockquote {
            font-size: 1.8rem;
        }

        /* Animation */
        @keyframes slide-in-left {
            from {
                transform: translateX(400px);
                opacity: 0;
            }

            to {
                transform: translateX(0);
                opacity: 1;
            }
        }

        #chat li:not(:last-of-type) {
            opacity: 0.5;
        }

        #chat li:last-of-type {
            animation-name: slide-in-left;
            animation-duration: 0.15s;
            animation-timing-function: ease-in;
        }
    </style>
</head>

<body>
    <div id="chat">
        <ul>
        </ul>
    </div>
</body>

<script>
    var chat = document.querySelector("#chat>ul");

    ComfyJS.onChat = (user, message, flags, self, extra) => {
        var newMessage = document.createElement("li");

        if (message.mod) {
            newMessage.classList.add('mod');
        }

        if (message.subscriber) {
            newMessage.classList.add('sub');
        }

        var text = document.createElement("blockquote");

        newMessage.innerText = user;
        text.innerText = message;

        newMessage.append(text);
        chat.append(newMessage);
    }

    ComfyJS.Init("skunkVT");
</script>

</html>
