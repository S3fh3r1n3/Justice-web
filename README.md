
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Justicia Digital - Juicio por Videollamada</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <header>
            <h1>🔍 Justicia Digital</h1>
            <p>Sistema de denuncias con juicio por videollamada y verificación por IA</p>
        </header>

        <!-- Formulario de Denuncia -->
        <section id="denuncia-section" class="active">
            <h2>Formulario de Denuncia</h2>
            <form id="denuncia-form">
                <div class="form-group">
                    <label for="denunciante">Tu nombre:</label>
                    <input type="text" id="denunciante" required>
                </div>
                
                <div class="form-group">
                    <label for="cuenta-acusada">Enlace a la cuenta denunciada (Facebook, Twitter, Instagram, etc.):</label>
                    <input type="url" id="cuenta-acusada" placeholder="https://twitter.com/usuario" required>
                </div>
                
                <div class="form-group">
                    <label for="motivo">Motivo de la denuncia:</label>
                    <select id="motivo" required>
                        <option value="">Seleccione...</option>
                        <option value="acoso">Acoso digital</option>
                        <option value="suplantacion">Suplantación de identidad</option>
                        <option value="discurso-odio">Discurso de odio</option>
                        <option value="spam">Spam o phishing</option>
                        <option value="otros">Otros</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="descripcion">Descripción detallada:</label>
                    <textarea id="descripcion" rows="5" required></textarea>
                </div>
                
                <div class="form-group">
                    <label for="pruebas">Adjunta pruebas (capturas, videos, etc.):</label>
                    <input type="file" id="pruebas" multiple accept="image/*, video/*, .pdf">
                    <div id="preview-container"></div>
                </div>
                
                <div class="legal-warning">
                    <p>⚠️ Al enviar esta denuncia, aceptas que:</p>
                    <ul>
                        <li>Se notificará al usuario denunciado</li>
                        <li>Participarás en un juicio digital por videollamada</li>
                        <li>Si el acusado es declarado culpable, su cuenta será suspendida</li>
                    </ul>
                </div>
                
                <button type="submit" class="btn-denuncia">Enviar Denuncia</button>
            </form>
        </section>

        <!-- Sala del Tribunal Digital -->
        <section id="tribunal-section" class="hidden">
            <div class="tribunal-header">
                <h2>⚖️ Tribunal Digital</h2>
                <div class="case-id">Caso #<span id="case-number"></span></div>
            </div>
            
            <div class="tribunal-layout">
                <div class="participant judge">
                    <div class="avatar">🤖</div>
                    <h3>Juez IA</h3>
                    <div class="ai-message" id="ai-message">"Analizando la denuncia inicial..."</div>
                    <div class="ai-loading">
                        <div class="loading-bar"></div>
                    </div>
                </div>
                
                <div class="video-container">
                    <div class="video-main" id="main-video">
                        <div class="video-label">Sala principal</div>
                    </div>
                    
                    <div class="participants-grid">
                        <div class="participant-card denunciante">
                            <div class="video-placeholder">
                                <div class="video-label">Denunciante</div>
                            </div>
                            <div class="participant-status" id="denunciante-status">No conectado</div>
                        </div>
                        
                        <div class="participant-card acusado">
                            <div class="video-placeholder">
                                <div class="video-label">Acusado</div>
                            </div>
                            <div class="participant-status" id="acusado-status">Citación pendiente</div>
                        </div>
                        
                        <div class="participant-card testigo hidden">
                            <div class="video-placeholder">
                                <div class="video-label">Testigo</div>
                            </div>
                            <div class="participant-status">No presente</div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="trial-controls">
                <button id="join-btn" class="btn-tribunal">Unirme a Videollamada</button>
                <button id="start-btn" class="btn-tribunal" disabled>Iniciar Juicio</button>
                <button id="witness-btn" class="btn-tribunal" disabled>Llamar Testigo</button>
                <button id="evidence-btn" class="btn-tribunal" disabled>Presentar Pruebas</button>
                <button id="verdict-btn" class="btn-tribunal" disabled>Concluir Juicio</button>
            </div>
            
            <div class="trial-log">
                <h3>📜 Registro del Juicio</h3>
                <div class="log-content" id="trial-log"></div>
            </div>
        </section>

        <!-- Veredicto Final -->
        <section id="veredicto-section" class="hidden">
            <div class="veredicto-header">
                <h2>Veredicto Final</h2>
                <div class="case-id">Caso #<span id="veredicto-case-number"></span></div>
            </div>
            
            <div class="veredicto-content" id="veredicto-content">
                <!-- Se llena dinámicamente -->
            </div>
            
            <div class="veredicto-actions">
                <button id="new-case-btn" class="btn-veredicto">Iniciar Nueva Denuncia</button>
            </div>
        </section>
    </div>

    <script src="script.js"></script>
</body>
</html>

:root {
    --primary: #2c3e50;
    --secondary: #3498db;
    --danger: #e74c3c;
    --success: #27ae60;
    --warning: #f39c12;
    --light: #ecf0f1;
    --dark: #2c3e50;
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    line-height: 1.6;
    color: #333;
    background-color: #f5f7fa;
    padding: 20px;
}

.container {
    max-width: 1000px;
    margin: 0 auto;
    background-color: white;
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
    overflow: hidden;
}

header {
    background-color: var(--primary);
    color: white;
    padding: 30px;
    text-align: center;
}

header h1 {
    font-size: 2.2rem;
    margin-bottom: 10px;
}

header p {
    opacity: 0.9;
}

section {
    padding: 30px;
}

.hidden {
    display: none;
}

/* Formulario de denuncia */
.form-group {
    margin-bottom: 20px;
}

label {
    display: block;
    margin-bottom: 8px;
    font-weight: 600;
}

input, select, textarea {
    width: 100%;
    padding: 12px;
    border: 1px solid #ddd;
    border-radius: 5px;
    font-family: inherit;
    font-size: 1rem;
}

textarea {
    min-height: 120px;
    resize: vertical;
}

.legal-warning {
    background-color: #fff8e1;
    padding: 15px;
    border-radius: 5px;
    margin: 20px 0;
    border-left: 4px solid var(--warning);
}

.legal-warning p {
    font-weight: 600;
    margin-bottom: 10px;
}

.legal-warning ul {
    padding-left: 20px;
}

.btn-denuncia {
    background-color: var(--danger);
    color: white;
    border: none;
    padding: 15px 30px;
    border-radius: 5px;
    font-size: 1.1rem;
    cursor: pointer;
    width: 100%;
    transition: background-color 0.3s;
}

.btn-denuncia:hover {
    background-color: #c0392b;
}

/* Preview de archivos */
#preview-container {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    margin-top: 15px;
}

.preview-item {
    position: relative;
    width: 100px;
    height: 100px;
    border: 1px solid #ddd;
    border-radius: 5px;
    overflow: hidden;
}

.preview-item img, .preview-item video {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.remove-btn {
    position: absolute;
    top: 5px;
    right: 5px;
    background-color: rgba(231, 76, 60, 0.8);
    color: white;
    border: none;
    border-radius: 50%;
    width: 22px;
    height: 22px;
    cursor: pointer;
    font-weight: bold;
}

/* Tribunal Digital */
.tribunal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 30px;
    padding-bottom: 15px;
    border-bottom: 1px solid #eee;
}

.case-id {
    background-color: var(--primary);
    color: white;
    padding: 5px 15px;
    border-radius: 20px;
    font-size: 0.9rem;
}

.judge {
    text-align: center;
    margin-bottom: 30px;
}

.avatar {
    font-size: 3rem;
    margin-bottom: 10px;
}

.ai-message {
    background-color: var(--light);
    padding: 15px;
    border-radius: 8px;
    margin-top: 15px;
    font-style: italic;
    min-height: 60px;
}

.ai-loading {
    margin-top: 15px;
}

.loading-bar {
    height: 4px;
    background-color: #ddd;
    border-radius: 2px;
    overflow: hidden;
}

.loading-bar::after {
    content: '';
    display: block;
    height: 100%;
    width: 0;
    background-color: var(--secondary);
    animation: loading 2s infinite;
}

@keyframes loading {
    0% { width: 0; }
    100% { width: 100%; }
}

.video-container {
    margin: 30px 0;
}

.video-main {
    background-color: #333;
    height: 400px;
    border-radius: 8px;
    position: relative;
    margin-bottom: 15px;
}

.video-label {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.7);
    color: white;
    padding: 8px;
    text-align: center;
}

.participants-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 15px;
}

.participant-card {
    background-color: white;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    overflow: hidden;
}

.video-placeholder {
    background-color: #555;
    height: 150px;
    position: relative;
}

.participant-status {
    padding: 10px;
    text-align: center;
    font-size: 0.9rem;
    color: var(--dark);
}

.denunciante .video-placeholder {
    border-top: 4px solid var(--success);
}

.acusado .video-placeholder {
    border-top: 4px solid var(--danger);
}

.testigo .video-placeholder {
    border-top: 4px solid var(--warning);
}

.trial-controls {
    display: flex;
    justify-content: center;
    gap: 10px;
    margin: 30px 0;
    flex-wrap: wrap;
}

.btn-tribunal {
    padding: 12px 20px;
    border: none;
    border-radius: 5px;
    background-color: var(--primary);
    color: white;
    cursor: pointer;
    font-weight: 600;
    transition: background-color 0.3s;
}

.btn-tribunal:hover {
    background-color: #1a252f;
}

.btn-tribunal:disabled {
    background-color: #95a5a6;
    cursor: not-allowed;
}

#join-btn {
    background-color: var(--success);
}

#start-btn {
    background-color: var(--secondary);
}

#witness-btn {
    background-color: var(--warning);
}

#verdict-btn {
    background-color: var(--danger);
}

.trial-log {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    margin-top: 30px;
}

.log-content {
    max-height: 200px;
    overflow-y: auto;
    background-color: #f9f9f9;
    padding: 15px;
    border-radius: 5px;
    font-family: 'Courier New', monospace;
    font-size: 0.9rem;
    margin-top: 15px;
}

/* Veredicto */
.veredicto-header {
    text-align: center;
    margin-bottom: 30px;
}

.veredicto-content {
    background-color: white;
    padding: 30px;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    margin-bottom: 30px;
}

.veredicto-result {
    font-size: 1.2rem;
    line-height: 1.6;
    padding: 20px;
    background-color: var(--light);
    border-radius: 8px;
    margin-bottom: 30px;
    text-align: center;
}

.veredicto-guilty {
    border-left: 5px solid var(--danger);
}

.veredicto-innocent {
    border-left: 5px solid var(--success);
}

.veredicto-analysis {
    margin-bottom: 30px;
}

.veredicto-analysis h3 {
    color: var(--primary);
    margin-bottom: 15px;
    border-bottom: 1px solid #eee;
    padding-bottom: 10px;
}

.btn-veredicto {
    background-color: var(--primary);
    color: white;
    border: none;
    padding: 15px 30px;
    border-radius: 5px;
    font-size: 1.1rem;
    cursor: pointer;
    width: 100%;
    transition: background-color 0.3s;
}

.btn-veredicto:hover {
    background-color: #1a252f;
}

/* Responsive */
@media (max-width: 768px) {
    .video-main {
        height: 250px;
    }
    
    .trial-controls {
        flex-direction: column;
    }
    
    .btn-tribunal {
        width: 100%;
    }
}

document.addEventListener('DOMContentLoaded', function() {
    // Elementos del DOM
    const denunciaForm = document.getElementById('denuncia-form');
    const denunciaSection = document.getElementById('denuncia-section');
    const tribunalSection = document.getElementById('tribunal-section');
    const veredictoSection = document.getElementById('veredicto-section');
    
    // Estado de la aplicación
    let caso = {
        denunciante: '',
        cuentaAcusada: '',
        motivo: '',
        descripcion: '',
        pruebas: [],
        veredicto: null
    };
    
    // Inicialización
    setupEventListeners();
    
    // Configurar event listeners
    function setupEventListeners() {
        // Formulario de denuncia
        denunciaForm.addEventListener('submit', handleDenunciaSubmit);
        
        // Tribunal digital
        document.getElementById('join-btn').addEventListener('click', joinVideoCall);
        document.getElementById('start-btn').addEventListener('click', startTrial);
        document.getElementById('witness-btn').addEventListener('click', callWitness);
        document.getElementById('evidence-btn').addEventListener('click', presentEvidence);
        document.getElementById('verdict-btn').addEventListener('click', concludeTrial);
        
        // Veredicto
        document.getElementById('new-case-btn').addEventListener('click', resetSystem);
        
        // Manejo de archivos
        document.getElementById('pruebas').addEventListener('change', handleFileUpload);
    }
    
    // Manejar envío de denuncia
    function handleDenunciaSubmit(e) {
        e.preventDefault();
        
        // Recoger datos del formulario
        caso.denunciante = document.getElementById('denunciante').value;
        caso.cuentaAcusada = document.getElementById('cuenta-acusada').value;
        caso.motivo = document.getElementById('motivo').value;
        caso.descripcion = document.getElementById('descripcion').value;
        
        // Validar que hay al menos una prueba
        if (caso.pruebas.length === 0) {
            alert('Por favor adjunta al menos una prueba');
            return;
        }
        
        // Mostrar tribunal
        denunciaSection.classList.remove('active');
        denunciaSection.classList.add('hidden');
        tribunalSection.classList.remove('hidden');
        
        // Generar número de caso
        const caseNumber = 'JD-' + Math.floor(Math.random() * 9000 + 1000);
        document.getElementById('case-number').textContent = caseNumber;
        document.getElementById('veredicto-case-number').textContent = caseNumber;
        
        // Iniciar proceso judicial
        startJudicialProcess();
    }
    
    // Manejar subida de archivos
    function handleFileUpload(e) {
        const files = e.target.files;
        const previewContainer = document.getElementById('preview-container');
        previewContainer.innerHTML = '';
        
        if (files) {
            caso.pruebas = Array.from(files);
            
            Array.from(files).forEach(file => {
                const previewItem = document.createElement('div');
                previewItem.className = 'preview-item';
                
                if (file.type.startsWith('image/')) {
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        const img = document.createElement('img');
                        img.src = e.target.result;
                        previewItem.appendChild(img);
                        addRemoveButton(previewItem, file);
                    }
                    reader.readAsDataURL(file);
                } 
                else if (file.type.startsWith('video/')) {
                    const video = document.createElement('video');
                    video.controls = true;
                    const source = document.createElement('source');
                    source.src = URL.createObjectURL(file);
                    source.type = file.type;
                    video.appendChild(source);
                    previewItem.appendChild(video);
                    addRemoveButton(previewItem, file);
                } 
                else {
                    const fileInfo = document.createElement('div');
                    fileInfo.style.padding = '10px';
                    fileInfo.textContent = file.name;
                    previewItem.appendChild(fileInfo);
                    addRemoveButton(previewItem, file);
                }
                
                previewItem.appendChild(createRemoveButton(file));
                previewContainer.appendChild(previewItem);
            });
        }
    }
    
    function createRemoveButton(file) {
        const removeBtn = document.createElement('button');
        removeBtn.className = 'remove-btn';
        removeBtn.innerHTML = '×';
        removeBtn.addEventListener('click', (e) => {
            e.preventDefault();
            e.stopPropagation();
            removeBtn.parentElement.remove();
            
            // Actualizar lista de archivos
            caso.pruebas = caso.pruebas.filter(f => f !== file);
        });
        return removeBtn;
    }
    
    // Iniciar proceso judicial
    function startJudicialProcess() {
        addToLog(`Caso iniciado contra: ${caso.cuentaAcusada}`);
        addToLog(`Motivo: ${getMotivoText(caso.motivo)}`);
        
        // Simular conexión del denunciante
        setTimeout(() => {
            document.getElementById('denunciante-status').textContent = "Conectado";
            addToLog("Denunciante se ha unido a la videollamada");
            
            // Simular citación al acusado
            setTimeout(() => {
                document.getElementById('acusado-status').textContent = "Notificado";
                addToLog(`Notificación enviada a ${caso.cuentaAcusada}`);
                
                // Simular conexión del acusado
                setTimeout(() => {
                    document.getElementById('acusado-status').textContent = "Conectado";
                    addToLog("Acusado se ha unido a la videollamada");
                    
                    // Activar botones
                    document.getElementById('start-btn').disabled = false;
                    document.getElementById('join-btn').textContent = "Conectado";
                    document.getElementById('join-btn').disabled = true;
                    
                    // Mensaje del juez IA
                    simulateJudgeMessage("Tribunal listo para comenzar. Denunciante, puede presentar su caso.");
                }, 3000);
            }, 2000);
        }, 1500);
    }
    
    // Unirse a videollamada
    function joinVideoCall() {
        addToLog("Te has unido a la videollamada");
        document.getElementById('join-btn').textContent = "Conectado";
        document.getElementById('join-btn').disabled = true;
    }
    
    // Iniciar juicio
    function startTrial() {
        addToLog("Juicio oficialmente iniciado");
        document.getElementById('start-btn').disabled = true;
        document.getElementById('witness-btn').disabled = false;
        
        simulateJudgeMessage("Procederemos con las declaraciones iniciales.");
    }
    
    // Llamar testigo
    function callWitness() {
        const testigoElement = document.querySelector('.testigo');
        testigoElement.classList.remove('hidden');
        addToLog("Testigo citado a declarar");
        document.getElementById('witness-btn').disabled = true;
        document.getElementById('evidence-btn').disabled = false;
        
        setTimeout(() => {
            testigoElement.querySelector('.participant-status').textContent = "Conectado";
            addToLog("Testigo se ha unido a la videollamada");
            simulateJudgeMessage("Testigo, por favor describa lo que presenció.");
        }, 2000);
    }
    
    // Presentar pruebas
    function presentEvidence() {
        addToLog("Pruebas presentadas al tribunal");
        document.getElementById('evidence-btn').disabled = true;
        document.getElementById('verdict-btn').disabled = false;
        
        simulateJudgeMessage("Analizando las pruebas presentadas...");
        
        // Simular análisis de pruebas por IA
        setTimeout(() => {
            simulateJudgeMessage("Análisis de pruebas completado. Procederemos a deliberar.");
        }, 4000);
    }
    
    // Concluir juicio y mostrar veredicto
    function concludeTrial() {
        addToLog("Juicio concluido. Esperando veredicto...");
        tribunalSection.classList.add('hidden');
        veredictoSection.classList.remove('hidden');
        
        // Generar veredicto aleatorio (en realidad sería determinado por IA)
        caso.veredicto = Math.random() > 0.5 ? 'culpable' : 'inocente';
        deliverVerdict();
    }
    
    // Mostrar veredicto final
    function deliverVerdict() {
        const veredictoContent = document.getElementById('veredicto-content');
        
        if (caso.veredicto === 'culpable') {
            veredictoContent.innerHTML = `
                <div class="veredicto-result veredicto-guilty">
                    <h3>🚨 Veredicto: CULPABLE</h3>
                    <p>El acusado ha sido encontrado responsable de las acusaciones.</p>
                    <p>La cuenta ${caso.cuentaAcusada} será suspendida permanentemente.</p>
                </div>
                <div class="veredicto-analysis">
                    <h3>Análisis de la IA Judicial</h3>
                    <p>Nuestro sistema ha determinado con un 92% de confianza que el acusado violó los términos de servicio. Las pruebas presentadas fueron consistentes con el patrón de comportamiento denunciado.</p>
                    <p><strong>Acciones tomadas:</strong></p>
                    <ul>
                        <li>Cuenta suspendida permanentemente</li>
                        <li>Contenido infractor eliminado</li>
                        <li>Posible notificación a autoridades</li>
                    </ul>
                </div>
            `;
            
            // Simular "hackeo" de la cuenta (en realidad sería una suspensión)
            addToLog(`CUENTA SUSPENDIDA: ${caso.cuentaAcusada}`);
        } else {
            veredictoContent.innerHTML = `
                <div class="veredicto-result veredicto-innocent">
                    <h3>✅ Veredicto: INOCENTE</h3>
                    <p>El acusado ha sido absuelto de las acusaciones.</p>
                    <p>No se tomarán acciones contra la cuenta ${caso.cuentaAcusada}.</p>
                </div>
                <div class="veredicto-analysis">
                    <h3>Análisis de la IA Judicial</h3>
                    <p>Nuestro sistema encontró solo un 34% de probabilidad de que las acusaciones sean válidas. Las pruebas presentadas no fueron concluyentes o no violan los términos de servicio.</p>
                    <p><strong>Acciones tomadas:</strong></p>
                    <ul>
                        <li>No se aplicarán sanciones</li>
                        <li>Caso archivado</li>
                        <li>El denunciante puede apelar presentando nuevas pruebas</li>
                    </ul>
                </div>
            `;
        }
    }
    
    // Reiniciar sistema para nueva denuncia
    function resetSystem() {
        // Limpiar formulario
        denunciaForm.reset();
        document.getElementById('preview-container').innerHTML = '';
        
        // Resetear tribunal
        document.getElementById('denunciante-status').textContent = "No conectado";
        document.getElementById('acusado-status').textContent = "Citación pendiente";
        document.querySelector('.testigo').classList.add('hidden');
        document.getElementById('trial-log').innerHTML = '';
        document.getElementById('ai-message').textContent = '"Analizando la denuncia inicial..."';
        
        // Resetear botones
        document.getElementById('join-btn').textContent = "Unirme a Videollamada";
        document.getElementById('join-btn').disabled = false;
        document.getElementById('start-btn').disabled = true;
        document.getElementById('witness-btn').disabled = true;
        document.getElementById('evidence-btn').disabled = true;
        document.getElementById('verdict-btn').disabled = true;
        
        // Volver a sección inicial
        veredictoSection.classList.add('hidden');
        denunciaSection.classList.remove('hidden');
        denunciaSection.classList.add('active');
        
        // Resetear caso
        caso = {
            denunciante: '',
            cuentaAcusada: '',
            motivo: '',
            descripcion: '',
            pruebas: [],
            veredicto: null
        };
    }
    
    // Funciones auxiliares
    function addToLog(message) {
        const log = document.getElementById('trial-log');
        const entry = document.createElement('div');
        entry.textContent = `[${new Date().toLocaleTimeString()}] ${message}`;
        log.appendChild(entry);
        log.scrollTop = log.scrollHeight;
    }
    
    function simulateJudgeMessage(message) {
        const aiMessage = document.getElementById('ai-message');
        aiMessage.textContent = `"${message}"`;
        addToLog(`Juez IA: ${message}`);
    }
    
    function getMotivoText(motivo) {
        const motivos = {
            'acoso': 'Acoso digital',
            'suplantacion': 'Suplantación de identidad',
            'discurso-odio': 'Discurso de odio',
            'spam': 'Spam o phishing',
            'otros': 'Otros'
        };
        return motivos[motivo] || motivo;
    }
});
