<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Perfil de Autoconocimiento - Whetten & Cameron</title>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Work+Sans:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        :root { --primary: #1a4d2e; --accent: #ffd700; --bg: #faf8f3; --text: #2b2b2b; }
        body { font-family: 'Work Sans', sans-serif; background: var(--bg); color: var(--text); margin: 0; padding-bottom: 50px; }
        .header { background: var(--primary); color: white; padding: 2rem; text-align: center; border-bottom: 5px solid var(--accent); }
        .container { max-width: 850px; margin: 2rem auto; padding: 0 1.5rem; }
        
        /* Pantalla de Inicio */
        #welcome-screen { background: white; padding: 3rem; border-radius: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); }
        .welcome-content h2 { font-family: 'Playfair Display', serif; color: var(--primary); }
        .feature-list { list-style: none; padding: 0; }
        .feature-list li { margin-bottom: 10px; padding-left: 25px; position: relative; }
        .feature-list li::before { content: '✓'; position: absolute; left: 0; color: var(--primary); font-weight: bold; }

        /* Tabs y Contenido (Ocultos al inicio) */
        #app-content { display: none; }
        .tabs { display: flex; gap: 8px; margin-bottom: 20px; flex-wrap: wrap; }
        .tab { flex: 1; padding: 12px; background: #eee; border: none; border-radius: 10px; cursor: pointer; text-align: center; font-weight: 600; min-width: 150px; }
        .tab.active { background: var(--primary); color: white; }
        .tab-content { display: none; background: white; padding: 2.5rem; border-radius: 15px; box-shadow: 0 4px 15px rgba(0,0,0,0.05); }
        .tab-content.active { display: block; }

        /* Estilos de preguntas y botones */
        .question { border-bottom: 1px solid #eee; padding: 25px 0; }
        .options-container { display: flex; justify-content: space-between; margin-top: 15px; gap: 8px; }
        .opt-btn { flex: 1; padding: 12px; border: 2px solid #ddd; background: white; border-radius: 8px; cursor: pointer; font-weight: bold; }
        .opt-btn.selected { background: var(--primary); color: white; border-color: var(--primary); }
        .btn-start { background: var(--primary); color: white; border: none; padding: 1.5rem 3rem; border-radius: 12px; cursor: pointer; font-size: 1.2rem; font-weight: bold; display: block; margin: 2rem auto; }
        .btn-submit { background: var(--primary); color: white; border: none; padding: 1.5rem; border-radius: 12px; cursor: pointer; width: 100%; font-size: 1.2rem; font-weight: bold; margin-top: 30px; }
        .results-card { display: none; margin-top: 2rem; background: white; padding: 2.5rem; border-radius: 20px; border-top: 10px solid var(--primary); }
        .feedback-item { margin-bottom: 30px; padding: 20px; border-radius: 12px; background: #fdfdfd; border-left: 6px solid var(--primary); }
    </style>
</head>
<body>

<div class="header">
    <h1>Perfil de Autoconocimiento Profesional</h1>
    <p>Gestión de las Relaciones | Whetten & Cameron</p>
</div>

<div class="container">
    <div id="welcome-screen">
        <div class="welcome-content">
            <h2>Bienvenido a la Evaluación Diagnóstica</h2>
            <p>Esta herramienta evalúa tres dimensiones clave del autoconocimiento directivo basadas en el marco teórico de <strong>Whetten y Cameron (2014)</strong>.</p>
            
            <hr>
            
            <h4>Estructura del Ejercicio:</h4>
            <ul class="feature-list">
                <li><strong>Estilo Cognoscitivo:</strong> (18 ítems) Evalúa su forma de percibir y evaluar información.</li>
                <li><strong>Locus de Control:</strong> (29 ítems) Determina su expectativa de control sobre su destino.</li>
                <li><strong>Tolerancia a la Ambigüedad:</strong> (16 ítems) Mide su respuesta ante situaciones inciertas.</li>
            </ul>

            <div style="background: #fff3cd; padding: 15px; border-radius: 10px; border-left: 5px solid #ffc107; margin: 20px 0;">
                <strong>⏱ Tiempo estimado:</strong> 20 minutos.<br>
                <strong>🔒 Privacidad:</strong> Sus respuestas se procesan localmente y no se envían a ningún servidor.
            </div>

            <button class="btn-start" onclick="startApp()">COMENZAR EVALUACIÓN</button>
        </div>
    </div>

    <div id="app-content">
        <div class="tabs">
            <button class="tab active" onclick="switchTab(0)">Estilo Cognoscitivo</button>
            <button class="tab" onclick="switchTab(1)">Locus de Control</button>
            <button class="tab" onclick="switchTab(2)">Ambigüedad</button>
        </div>

        <form id="quizForm">
            <div class="tab-content active" id="tab0"><div id="cogBox"></div></div>
            <div class="tab-content" id="tab1"><div id="locBox"></div></div>
            <div class="tab-content" id="tab2"><div id="ambBox"></div></div>
            <button type="button" class="btn-submit" onclick="processResults()">Generar Diagnóstico Académico</button>
        </form>

        <div id="results" class="results-card">
            <h2 style="text-align:center; font-family: 'Playfair Display', serif;">Informe de Perfil Individual</h2>
            <div id="resOutput"></div>
            <button class="btn-submit" style="background:#444" onclick="window.print()">Imprimir o Guardar Reporte</button>
        </div>
    </div>
</div>

<script>
    // Lógica para mostrar la app
    function startApp() {
        document.getElementById('welcome-screen').style.display = 'none';
        document.getElementById('app-content').style.display = 'block';
        window.scrollTo(0,0);
    }

    // [Aquí se mantienen todas las constantes cogQs, locQs, ambQs y las funciones init(), setVal(), processResults() del código anterior]
    // ... (Mantén el resto del código JavaScript que ya teníamos para que funcionen las preguntas)
</script>
</body>
</html>
