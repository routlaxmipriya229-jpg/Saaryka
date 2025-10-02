<!DOCTYPE html>
<html>
<head>
  <title>Mini Chat App</title>
  <style>
    body { font-family: Arial; }
    #messages { height: 300px; overflow-y: scroll; border: 1px solid #ccc; padding: 10px; }
    input { padding: 8px; width: 70%; }
    button { padding: 8px; }
  </style>
</head>
<body>
  <h2>🔥 Mini Chat</h2>
  <div id="messages"></div>
  <input id="msgInput" placeholder="Type message..."/>
  <button onclick="sendMessage()">Send</button>

  <!-- Firebase SDK -->
  <script src="https://www.gstatic.com/firebasejs/9.1.3/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.1.3/firebase-database.js"></script>

  <script>
    // 1. Your Firebase config (replace with your project’s keys)
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_PROJECT.firebaseapp.com",
      databaseURL: "https://YOUR_PROJECT.firebaseio.com",
      projectId: "YOUR_PROJECT",
      storageBucket: "YOUR_PROJECT.appspot.com",
      messagingSenderId: "YOUR_SENDER_ID",
      appId: "YOUR_APP_ID"
    };

    // 2. Initialize
    const app = firebase.initializeApp(firebaseConfig);
    const db = firebase.database();

    // 3. Send message
    function sendMessage() {
      const msg = document.getElementById("msgInput").value;
      db.ref("messages").push().set({ text: msg });
      document.getElementById("msgInput").value = "";
    }

    // 4. Listen for new messages
    db.ref("messages").on("child_added", function(snapshot) {
      let msgBox = document.getElementById("messages");
      msgBox.innerHTML += "<p>" + snapshot.val().text + "</p>";
    });
  </script>
</body>
</html>
