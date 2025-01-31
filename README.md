<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiniela de Fútbol</title>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-firestore.js"></script>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; }
        .container { width: 300px; margin: auto; }
        button { background-color: #28a745; color: white; padding: 10px; border: none; cursor: pointer; }
    </style>
</head>
<body>
    <div class="container">
        <h2>Quiniela de Fútbol</h2>
        <label>Partido 1: </label>
        <select id="partido1">
            <option value="Equipo A">Equipo A</option>
            <option value="Empate">Empate</option>
            <option value="Equipo B">Equipo B</option>
        </select>
        <br><br>
        <label>Partido 2: </label>
        <select id="partido2">
            <option value="Equipo C">Equipo C</option>
            <option value="Empate">Empate</option>
            <option value="Equipo D">Equipo D</option>
        </select>
        <br><br>
        <button onclick="enviarQuiniela()">Enviar Quiniela</button>
        <br><br>
        <a id="whatsappLink" href="#" target="_blank">Enviar por WhatsApp</a>
    </div>

    <script>
        // Configuración de Firebase
        const firebaseConfig = {
            apiKey: "TU_API_KEY",
            authDomain: "TU_AUTH_DOMAIN",
            projectId: "TU_PROJECT_ID",
            storageBucket: "TU_STORAGE_BUCKET",
            messagingSenderId: "TU_MESSAGING_SENDER_ID",
            appId: "TU_APP_ID"
        };
        
        firebase.initializeApp(firebaseConfig);
        const db = firebase.firestore();
        
        function enviarQuiniela() {
            const partido1 = document.getElementById("partido1").value;
            const partido2 = document.getElementById("partido2").value;
            
            db.collection("quinielas").add({
                partido1: partido1,
                partido2: partido2,
                timestamp: new Date()
            }).then(() => {
                alert("Quiniela enviada con éxito!");
                generarWhatsAppLink(partido1, partido2);
            });
        }
        
        function generarWhatsAppLink(p1, p2) {
            const mensaje = `Mis selecciones en la quiniela: \nPartido 1: ${p1} \nPartido 2: ${p2}`;
            const url = `https://wa.me/?text=${encodeURIComponent(mensaje)}`;
            document.getElementById("whatsappLink").href = url;
        }
    </script>
</body>
</html>
