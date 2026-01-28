<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome to the Matrix</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Courier New', monospace;
        }

        body {
            background-color: #000;
            color: #0f0;
            overflow-x: hidden;
            min-height: 100vh;
            position: relative;
        }

        /* Efeito de chuva de código Matrix */
        #matrix-rain {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            opacity: 0.3;
            z-index: 1;
        }

        .matrix-char {
            position: absolute;
            color: #0f0;
            font-size: 14px;
            animation: fall linear infinite;
        }

        @keyframes fall {
            to { transform: translateY(100vh); }
        }

        /* Container principal */
        .container {
            position: relative;
            z-index: 2;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        /* Header */
        .header {
            text-align: center;
            padding: 40px 20px;
            border: 2px solid #0f0;
            margin-bottom: 40px;
            position: relative;
            background: rgba(0, 0, 0, 0.8);
        }

        .header::before {
            content: '';
            position: absolute;
            top: -2px;
            left: -2px;
            right: -2px;
            bottom: -2px;
            background: linear-gradient(45deg, #0f0, #090, #0f0);
            z-index: -1;
            filter: blur(10px);
            opacity: 0.5;
        }

        .matrix-title {
            font-size: 3.5rem;
            color: #0f0;
            text-shadow: 0 0 10px #0f0;
            margin-bottom: 20px;
            letter-spacing: 3px;
        }

        .subtitle {
            color: #8f8;
            font-size: 1.2rem;
            margin-bottom: 30px;
        }

        /* Code block */
        .code-block {
            background: rgba(0, 20, 0, 0.7);
            border: 1px solid #0f0;
            border-radius: 5px;
            padding: 25px;
            margin: 30px 0;
            position: relative;
            overflow: hidden;
        }

        .code-block::before {
            content: '>>_';
            position: absolute;
            top: 10px;
            left: 10px;
            color: #0f0;
            font-weight: bold;
        }

        .diff-code {
            color: #0f0;
            line-height: 1.6;
            font-size: 1.1rem;
        }

        .diff-add {
            color: #0f0;
        }

        /* Sections */
        .section {
            background: rgba(0, 30, 0, 0.3);
            border-left: 4px solid #0f0;
            padding: 25px;
            margin: 30px 0;
            transition: transform 0.3s;
        }

        .section:hover {
            transform: translateX(10px);
            box-shadow: 0 0 20px rgba(0, 255, 0, 0.2);
        }

        .section-title {
            color: #0f0;
            font-size: 1.8rem;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .section-title::before {
            content: '>_';
            color: #0f0;
        }

        /* Stack Grid */
        .stack-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .stack-card {
            background: rgba(0, 40, 0, 0.4);
            border: 1px solid #0a0;
            padding: 20px;
            border-radius: 5px;
            transition: all 0.3s;
        }

        .stack-card:hover {
            background: rgba(0, 60, 0, 0.6);
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(0, 255, 0, 0.3);
        }

        .stack-category {
            color: #8f8;
            font-size: 1.2rem;
            margin-bottom: 15px;
            border-bottom: 1px solid #0a0;
            padding-bottom: 5px;
        }

        .stack-list {
            list-style: none;
        }

        .stack-list li {
            padding: 8px 0;
            border-bottom: 1px dashed #060;
            position: relative;
            padding-left: 25px;
        }

        .stack-list li::before {
            content: '▷';
            position: absolute;
            left: 0;
            color: #0f0;
        }

        /* Status */
        .status-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .status-item {
            background: rgba(0, 30, 0, 0.5);
            padding: 15px;
            text-align: center;
            border: 1px solid #0a0;
            border-radius: 3px;
            position: relative;
            overflow: hidden;
        }

        .status-item::after {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(0, 255, 0, 0.2), transparent);
            transition: left 0.5s;
        }

        .status-item:hover::after {
            left: 100%;
        }

        .status-ok {
            color: #0f0;
            font-weight: bold;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        /* Stats */
        .stats-container {
            display: flex;
            justify-content: center;
            gap: 30px;
            flex-wrap: wrap;
            margin: 40px 0;
        }

        .stat-box {
            text-align: center;
            padding: 20px;
            min-width: 200px;
            background: rgba(0, 40, 0, 0.5);
            border: 1px solid #0a0;
            border-radius: 5px;
        }

        .stat-number {
            font-size: 2.5rem;
            color: #0f0;
            text-shadow: 0 0 10px #0f0;
        }

        .stat-label {
            color: #8f8;
            margin-top: 10px;
        }

        /* Footer */
        .footer {
            text-align: center;
            padding: 40px 20px;
            margin-top: 50px;
            border-top: 1px solid #0a0;
        }

        .quote {
            font-style: italic;
            color: #8f8;
            margin-bottom: 30px;
            font-size: 1.2rem;
        }

        .cta-button {
            display: inline-block;
            padding: 15px 40px;
            background: transparent;
            border: 2px solid #0f0;
            color: #0f0;
            text-decoration: none;
            font-size: 1.1rem;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
            margin-top: 20px;
        }

        .cta-button:hover {
            background: rgba(0, 255, 0, 0.1);
            box-shadow: 0 0 20px rgba(0, 255, 0, 0.3);
            transform: scale(1.05);
        }

        /* Glitch effect */
        .glitch {
            position: relative;
            animation: glitch 5s infinite;
        }

        @keyframes glitch {
            0%, 100% { transform: translate(0); }
            1% { transform: translate(-2px, 2px); }
            2% { transform: translate(2px, -2px); }
            3% { transform: translate(-2px, -2px); }
            4% { transform: translate(2px, 2px); }
            5% { transform: translate(0); }
        }

        /* Responsive */
        @media (max-width: 768px) {
            .matrix-title {
                font-size: 2.5rem;
            }
            
            .stack-grid {
                grid-template-columns: 1fr;
            }
            
            .status-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .stats-container {
                flex-direction: column;
                align-items: center;
            }
        }
    </style>
</head>
<body>
    <!-- Matrix Rain Effect -->
    <div id="matrix-rain"></div>

    <div class="container">
        <!-- Header -->
        <header class="header glitch">
            <h1 class="matrix-title">WELCOME TO THE MATRIX</h1>
            <p class="subtitle">Cada linha de código é uma escolha. Cada escolha define a realidade.</p>
        </header>

        <!-- Code Section -->
        <div class="code-block">
            <pre class="diff-code"><code><span class="diff-add">+ Desenvolvedor fullstack</span>
<span class="diff-add">+ Cada linha de código é uma escolha</span>

while(alive) {
   learn();
   code();
   breakTheMatrix();
}</code></pre>
        </div>

        <!-- About Section -->
        <section class="section">
            <h2 class="section-title">SOBRE MIM</h2>
            <p>Sou um desenvolvedor focado em lógica, performance e arquitetura. 
               Gosto de entender como os sistemas funcionam por trás da interface 
               e transformar problemas complexos em soluções simples e eficientes.</p>
            <p>Acredito que cada linha de código escrita molda a realidade digital.</p>
        </section>

        <!-- Stack Section -->
        <section class="section">
            <h2 class="section-title">STACK PRINCIPAL</h2>
            <div class="stack-grid">
                <div class="stack-card">
                    <h3 class="stack-category">LINGUAGENS</h3>
                    <ul class="stack-list">
                        <li>Java</li>
                        <li>C#</li>
                        <li>C</li>
                        <li>Python</li>
                        <li>JavaScript</li>
                    </ul>
                </div>
                
                <div class="stack-card">
                    <h3 class="stack-category">FRONT-END</h3>
                    <ul class="stack-list">
                        <li>HTML</li>
                        <li>CSS</li>
                        <li>Angular</li>
                    </ul>
                </div>
                
                <div class="stack-card">
                    <h3 class="stack-category">BACK-END</h3>
                    <ul class="stack-list">
                        <li>Node.js</li>
                        <li>APIs REST</li>
                        <li>Microserviços</li>
                    </ul>
                </div>
                
                <div class="stack-card">
                    <h3 class="stack-category">CONHECIMENTOS</h3>
                    <ul class="stack-list">
                        <li>Clean Code</li>
                        <li>Arquitetura de Software</li>
                        <li>Git & GitHub</li>
                        <li>CI/CD</li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- Status Section -->
        <section class="section">
            <h2 class="section-title">STATUS DA MATRIX</h2>
            <p>Inicializando sistema... Carregando módulos...</p>
            
            <div class="status-grid">
                <div class="status-item">
                    <span class="status-ok">[OK]</span> Java
                </div>
                <div class="status-item">
                    <span class="status-ok">[OK]</span> C#
                </div>
                <div class="status-item">
                    <span class="status-ok">[OK]</span> C
                </div>
                <div class="status-item">
                    <span class="status-ok">[OK]</span> Python
                </div>
                <div class="status-item">
                    <span class="status-ok">[OK]</span> JavaScript
                </div>
                <div class="status-item">
                    <span class="status-ok">[OK]</span> Node.js
                </div>
                <div class="status-item">
                    <span class="status-ok">[OK]</span> Angular
                </div>
            </div>
            
            <p style="margin-top: 20px; color: #0f0; font-weight: bold;">STATUS: CONECTADO À MATRIX</p>
        </section>

        <!-- Stats Section -->
        <section class="section">
            <h2 class="section-title">ESTATÍSTICAS DO SISTEMA</h2>
            <div class="stats-container">
                <div class="stat-box">
                    <div class="stat-number">7+</div>
                    <div class="stat-label">Linguagens</div>
                </div>
                <div class="stat-box">
                    <div class="stat-number">100%</div>
                    <div class="stat-label">Código Limpo</div>
                </div>
                <div class="stat-box">
                    <div class="stat-number">∞</div>
                    <div class="stat-label">Possibilidades</div>
                </div>
            </div>
        </section>

        <!-- Final Section -->
        <section class="section">
            <h2 class="section-title">CÓDIGO DE VIDA</h2>
            <div class="code-block">
                <pre class="diff-code"><code>def break_the_matrix():
    while is_alive():
        learn_new_tech()
        write_clean_code()
        solve_complex_problems()
        repeat()
    
    return legacy()

# A realidade é escrita em linhas de código</code></pre>
            </div>
        </section>

        <!-- Footer -->
        <footer class="footer">
            <p class="quote">"Não tente entender o código. Seja o código."</p>
            <p style="color: #0f0; font-size: 1.5rem; margin: 20px 0;">A REALIDADE É ESCRITA EM LINHAS DE CÓDIGO.</p>
            
            <a href="https://github.com/SEU_USERNAME" class="cta-button" target="_blank">
                ENTRAR NA MATRIX
            </a>
            
            <p style="margin-top: 30px; color: #8f8;">© 2024 - Todos os códigos são realidade.</p>
        </footer>
    </div>

    <script>
        // Matrix Rain Effect
        function createMatrixRain() {
            const container = document.getElementById('matrix-rain');
            const chars = '01アイウエオカキクケコサシスセソタチツテトナニヌネノハヒフヘホマミムメモヤユヨラリルレロワヲン';
            
            for (let i = 0; i < 100; i++) {
                const char = document.createElement('div');
                char.className = 'matrix-char';
                char.textContent = chars[Math.floor(Math.random() * chars.length)];
                char.style.left = Math.random() * 100 + 'vw';
                char.style.animationDuration = (Math.random() * 5 + 3) + 's';
                char.style.animationDelay = Math.random() * 5 + 's';
                char.style.opacity = Math.random() * 0.5 + 0.3;
                container.appendChild(char);
            }
        }

        // Typing effect for titles
        function typeEffect(element, text, speed = 100) {
            let i = 0;
            element.textContent = '';
            
            function type() {
                if (i < text.length) {
                    element.textContent += text.charAt(i);
                    i++;
                    setTimeout(type, speed);
                }
            }
            
            type();
        }

        // Status animation
        function animateStatus() {
            const statusItems = document.querySelectorAll('.status-ok');
            statusItems.forEach((item, index) => {
                setTimeout(() => {
                    item.style.animation = 'none';
                    setTimeout(() => {
                        item.style.animation = 'pulse 2s infinite';
                    }, 50);
                }, index * 300);
            });
        }

        // Initialize effects
        document.addEventListener('DOMContentLoaded', () => {
            createMatrixRain();
            
            // Animate main title
            const title = document.querySelector('.matrix-title');
            const originalTitle = title.textContent;
            typeEffect(title, originalTitle, 150);
            
            // Animate status periodically
            setInterval(animateStatus, 5000);
            
            // Glitch effect random
            setInterval(() => {
                const glitch = document.querySelector('.glitch');
                glitch.style.animation = 'none';
                setTimeout(() => {
                    glitch.style.animation = 'glitch 5s infinite';
                }, 100);
            }, 10000);
        });

        // Interactive code blocks
        document.querySelectorAll('.code-block').forEach(block => {
            block.addEventListener('click', () => {
                block.style.transform = 'scale(1.02)';
                setTimeout(() => {
                    block.style.transform = 'scale(1)';
                }, 300);
            });
        });
    </script>
</body>
</html>
