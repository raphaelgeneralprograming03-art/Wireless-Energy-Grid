
<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>S.R.O.S. - Redes de Energia Planetária Inesgotável (Sem Fios)</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        space: {
                            950: '#020617',
                            900: '#030712',
                            800: '#0b0f19',
                            700: '#111827',
                        },
                        quantum: {
                            cyan: '#00f3ff',
                            emerald: '#10b981',
                            amber: '#f59e0b',
                            violet: '#8b5cf6',
                            rose: '#f43f5e'
                        }
                    },
                    fontFamily: {
                        mono: ['JetBrains Mono', 'Courier New', monospace],
                        orbitron: ['Orbitron', 'sans-serif']
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Orbitron:wght@500;700;900&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            font-family: 'JetBrains Mono', monospace;
            background-color: #020617;
            color: #f8fafc;
            overflow-x: hidden;
        }
        h1, h2, h3, .font-orbitron {
            font-family: 'Orbitron', sans-serif;
        }
        .glow-cyan {
            box-shadow: 0 0 25px rgba(0, 243, 255, 0.35);
        }
        .glow-emerald {
            box-shadow: 0 0 25px rgba(16, 185, 129, 0.35);
        }
        .text-glow-cyan {
            text-shadow: 0 0 12px rgba(0, 243, 255, 0.8);
        }
        .scanline {
            background: linear-gradient(
                to bottom,
                rgba(255,255,255,0),
                rgba(255,255,255,0) 50%,
                rgba(0, 243, 255, 0.03) 50%,
                rgba(0, 243, 255, 0.03)
            );
            background-size: 100% 4px;
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #030712;
        }
        ::-webkit-scrollbar-thumb {
            background: #111827;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #00f3ff;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col bg-space-950 scanline">

    <header class="border-b border-quantum-cyan/30 bg-space-900/90 backdrop-blur-md sticky top-0 z-50 px-4 py-3">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4">
            
            <div class="flex items-center space-x-3">
                <div class="w-10 h-10 rounded-xl bg-space-800 border border-quantum-cyan flex items-center justify-center glow-cyan">
                    <i class="fa-solid fa-atom text-quantum-cyan text-xl animate-spin" style="animation-duration: 8s;"></i>
                </div>
                <div>
                    <h1 class="text-xl font-black tracking-wider text-quantum-cyan text-glow-cyan">S.R.O.S. - POWER GRID</h1>
                    <p class="text-[10px] text-slate-400 uppercase tracking-widest">Rede de Energia Quântica Sem Fios</p>
                </div>
            </div>

            <!-- View Modes & Tabs -->
            <div class="flex flex-wrap items-center gap-1.5 bg-space-950/80 p-1.5 rounded-xl border border-space-800">
                <button onclick="switchView('global')" id="tab-global" class="px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all bg-quantum-cyan/25 text-quantum-cyan border border-quantum-cyan/60 glow-cyan flex items-center gap-2">
                    <i class="fa-solid fa-globe"></i> Visão Orbital Global
                </button>
                <button onclick="switchView('quantum')" id="tab-quantum" class="px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all text-slate-400 hover:text-quantum-cyan hover:bg-space-800 border border-transparent flex items-center gap-2">
                    <i class="fa-solid fa-bolt"></i> Rotor de Vácuo Quântico
                </button>
                <button onclick="switchView('cities')" id="tab-cities" class="px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all text-slate-400 hover:text-quantum-cyan hover:bg-space-800 border border-transparent flex items-center gap-2">
                    <i class="fa-solid fa-city"></i> Cidades Alimentadas
                </button>
            </div>

            <!-- Action Buttons -->
            <div class="flex items-center space-x-3">
                <button onclick="toggleAudio()" id="btn-audio" class="w-9 h-9 rounded-xl bg-space-800 border border-space-700 hover:border-quantum-cyan text-slate-300 flex items-center justify-center text-xs transition-all" title="Alternar Som Ambiente">
                    <i class="fa-solid fa-volume-xmark" id="audio-icon"></i>
                </button>
                <button onclick="openModal()" class="px-3 py-1.5 rounded-xl bg-space-800 border border-quantum-cyan/40 hover:border-quantum-cyan text-quantum-cyan text-xs font-bold flex items-center gap-2 transition-all glow-cyan">
                    <i class="fa-solid fa-book-open"></i> Visão Geral do Aplicativo
                </button>
            </div>
        </div>
    </header>

    <main class="flex-1 max-w-7xl w-full mx-auto p-4 grid grid-cols-1 lg:grid-cols-4 gap-4">
        
        <!-- Canvas Area (3 Cols) -->
        <div class="lg:col-span-3 flex flex-col gap-4">
            
            <div class="relative w-full aspect-[16/10] bg-space-900 rounded-2xl border border-quantum-cyan/30 overflow-hidden glow-cyan flex items-center justify-center">
                
                <!-- Main Canvas Element -->
                <canvas id="simCanvas" class="w-full h-full block cursor-crosshair"></canvas>

                <!-- Floating HUD Overlays -->
                <div class="absolute top-4 left-4 bg-space-950/85 backdrop-blur-md p-3 rounded-xl border border-quantum-cyan/30 text-xs space-y-1 pointer-events-none">
                    <div class="text-quantum-cyan font-bold uppercase tracking-wider flex items-center gap-2">
                        <i class="fa-solid fa-satellite animate-pulse"></i> <span id="hud-title">MODO: TRANSMISSÃO FULL DUPLEX ATIVA</span>
                    </div>
                    <div class="text-slate-400">FPS: <span id="hud-fps" class="text-white">60</span> | ESTAÇÃO SROS: <span id="hud-station" class="text-emerald-400">Órbita Baixa (LEO)</span></div>
                    <div class="text-slate-400">ALINHAMENTO LASER: <span id="hud-align" class="text-quantum-cyan">99.98% (Estável)</span></div>
                </div>

                <!-- Interlock Warning Overlay -->
                <div id="interlock-alert" class="absolute top-4 right-4 bg-rose-950/90 backdrop-blur-md px-4 py-2 rounded-xl border border-rose-500 text-xs font-bold text-rose-300 hidden animate-pulse flex items-center gap-2">
                    <i class="fa-solid fa-triangle-exclamation"></i> INTERLOCK DE EMERGÊNCIA ATIVADO
                </div>

                <!-- Simulation Playback Controls Bar -->
                <div class="absolute bottom-4 left-1/2 -translate-x-1/2 bg-space-950/90 backdrop-blur-md px-6 py-3 rounded-2xl border border-quantum-cyan/40 flex items-center gap-4 shadow-2xl">
                    <button onclick="togglePlayPause()" id="btn-play" class="w-10 h-10 rounded-xl bg-quantum-cyan hover:bg-emerald-400 text-space-950 font-bold flex items-center justify-center transition-all glow-cyan">
                        <i class="fa-solid fa-pause" id="icon-play"></i>
                    </button>
                    <div class="h-6 w-[1px] bg-space-800"></div>
                    <div class="flex items-center gap-2">
                        <span class="text-xs text-slate-400 uppercase">Velocidade:</span>
                        <button onclick="setSpeed(1)" id="spd-1" class="px-2.5 py-1 rounded-lg text-xs font-bold bg-quantum-cyan/25 text-quantum-cyan border border-quantum-cyan">1x</button>
                        <button onclick="setSpeed(3)" id="spd-3" class="px-2.5 py-1 rounded-lg text-xs font-bold bg-space-800 text-slate-400 border border-space-700">3x</button>
                        <button onclick="setSpeed(5)" id="spd-5" class="px-2.5 py-1 rounded-lg text-xs font-bold bg-space-800 text-slate-400 border border-space-700">5x</button>
                    </div>
                    <div class="h-6 w-[1px] bg-space-800"></div>
                    <button onclick="triggerEmergencyCutoff()" class="px-3 py-1.5 rounded-xl bg-rose-950/80 hover:bg-rose-900 text-xs text-rose-300 border border-rose-500/50 flex items-center gap-2 transition-all font-bold">
                        <i class="fa-solid fa-power-off"></i> Corte de Emergência
                    </button>
                </div>
            </div>

            <!-- Description Box -->
            <div class="bg-space-900/90 backdrop-blur-md p-4 rounded-2xl border border-space-800 text-sm">
                <h3 class="font-bold text-quantum-cyan mb-1 flex items-center gap-2"><i class="fa-solid fa-circle-info"></i> Estado Atual da Rede Sem Fios</h3>
                <p id="view-desc" class="text-slate-300 text-xs leading-relaxed">
                    Naves SROS em órbita capturam energia limpa do vácuo quântico através de rotores em movimento circular. O feixe laser Full Duplex transmite os fótons com perda quase zero diretamente para as estações receptoras na Terra, iluminando metrópoles sem cabos.
                </p>
            </div>

        </div>

        <div class="lg:col-span-1 flex flex-col gap-4">
            
            <!-- Telemetry Panel -->
            <div class="bg-space-900/90 backdrop-blur-md p-4 rounded-2xl border border-quantum-cyan/30 flex flex-col gap-4">
                <div class="flex items-center justify-between border-b border-space-800 pb-3">
                    <h2 class="font-orbitron font-bold text-sm text-quantum-cyan flex items-center gap-2">
                        <i class="fa-solid fa-gauge-high"></i> Telemetria SROS
                    </h2>
                    <span class="text-[10px] bg-emerald-500/20 text-emerald-400 px-2 py-0.5 rounded border border-emerald-500/40">ONLINE</span>
                </div>

                <!-- Metrics -->
                <div class="space-y-3 text-xs">
                    <div>
                        <div class="flex justify-between mb-1">
                            <span class="text-slate-400">Energia Gerada (Vácuo)</span>
                            <span id="val-power" class="text-quantum-cyan font-bold">4,850 GW</span>
                        </div>
                        <div class="w-full bg-space-950 rounded-full h-2 overflow-hidden border border-space-800">
                            <div id="bar-power" class="bg-quantum-cyan h-full transition-all duration-300" style="width: 80%;"></div>
                        </div>
                    </div>

                    <div>
                        <div class="flex justify-between mb-1">
                            <span class="text-slate-400">Eficiência de Transmissão</span>
                            <span id="val-eff" class="text-emerald-400 font-bold">99.4%</span>
                        </div>
                        <div class="w-full bg-space-950 rounded-full h-2 overflow-hidden border border-space-800">
                            <div id="bar-eff" class="bg-emerald-400 h-full transition-all duration-300" style="width: 99.4%;"></div>
                        </div>
                    </div>

                    <div>
                        <div class="flex justify-between mb-1">
                            <span class="text-slate-400">Saturação da Rede Global</span>
                            <span id="val-grid" class="text-amber-400 font-bold">88.2%</span>
                        </div>
                        <div class="w-full bg-space-950 rounded-full h-2 overflow-hidden border border-space-800">
                            <div id="bar-grid" class="bg-amber-400 h-full transition-all duration-300" style="width: 88.2%;"></div>
                        </div>
                    </div>
                </div>

                <!-- City Power Grid Status -->
                <div class="pt-2 border-t border-space-800 space-y-2">
                    <h3 class="font-bold text-[11px] text-slate-400 uppercase tracking-wider">Cidades Conectadas</h3>
                    <div class="space-y-1.5 text-xs">
                        <div class="flex justify-between items-center bg-space-950 p-2 rounded-xl border border-space-800">
                            <span class="text-slate-300"><i class="fa-solid fa-city text-quantum-cyan mr-1.5"></i> Nova Tóquio</span>
                            <span class="text-emerald-400 font-bold">1,250 GW</span>
                        </div>
                        <div class="flex justify-between items-center bg-space-950 p-2 rounded-xl border border-space-800">
                            <span class="text-slate-300"><i class="fa-solid fa-city text-quantum-cyan mr-1.5"></i> São Paulo Prime</span>
                            <span class="text-emerald-400 font-bold">980 GW</span>
                        </div>
                        <div class="flex justify-between items-center bg-space-950 p-2 rounded-xl border border-space-800">
                            <span class="text-slate-300"><i class="fa-solid fa-city text-quantum-cyan mr-1.5"></i> Nova Alexandria</span>
                            <span class="text-emerald-400 font-bold">1,420 GW</span>
                        </div>
                    </div>
                </div>

                <!-- Controls -->
                <div class="space-y-3 pt-2 border-t border-space-800">
                    <h3 class="font-bold text-xs text-quantum-cyan uppercase">Controles de Operação</h3>
                    
                    <div class="space-y-1">
                        <div class="flex justify-between text-xs">
                            <span class="text-slate-400">Velocidade Rotor Quântico</span>
                            <span id="label-rotor" class="text-quantum-cyan font-bold">7,500 RPM</span>
                        </div>
                        <input type="range" id="rotorSlider" min="1000" max="10000" step="500" value="7500" 
                            class="w-full accent-quantum-cyan bg-space-950 rounded-lg appearance-none cursor-pointer h-2 border border-space-800"
                            oninput="updateRotorSpeed(this.value)">
                    </div>

                    <div class="flex items-center justify-between bg-space-950 p-2.5 rounded-xl border border-space-800">
                        <span class="text-xs text-slate-300">IA AutoNav & Gimbals</span>
                        <button onclick="toggleAutoAlign()" id="btn-align" class="px-3 py-1 rounded-lg text-xs font-bold bg-emerald-500/20 text-emerald-400 border border-emerald-500/50 glow-emerald transition-all">
                            LIGADO
                        </button>
                    </div>

                    <div class="space-y-1">
                        <div class="flex justify-between text-xs">
                            <span class="text-slate-400">Intensidade do Laser</span>
                            <span id="label-laser" class="text-amber-400 font-bold">Padrão (75%)</span>
                        </div>
                        <input type="range" id="laserSlider" min="25" max="100" step="25" value="75" 
                            class="w-full accent-amber-400 bg-space-950 rounded-lg appearance-none cursor-pointer h-2 border border-space-800"
                            oninput="updateLaserIntensity(this.value)">
                    </div>
                </div>

            </div>

            <!-- Terminal Log -->
            <div class="bg-space-900/90 backdrop-blur-md p-4 rounded-2xl border border-space-800 flex flex-col flex-1 min-h-[180px]">
                <div class="flex items-center justify-between border-b border-space-800 pb-2 mb-2">
                    <h3 class="font-orbitron font-bold text-xs text-quantum-cyan flex items-center gap-2">
                        <i class="fa-solid fa-terminal"></i> Log de Diagnóstico SROS
                    </h3>
                    <button onclick="clearLogs()" class="text-[10px] text-slate-400 hover:text-quantum-cyan underline">Limpar</button>
                </div>
                <div id="log-container" class="flex-1 overflow-y-auto space-y-1.5 font-mono text-[11px] text-slate-300 max-h-[160px]">
                    <div class="text-quantum-cyan">[08:22:00] SROS Grid inicializado em órbita LEO.</div>
                    <div class="text-emerald-400">[08:22:01] Extração quântica em movimento circular ativada.</div>
                    <div class="text-slate-400">[08:22:02] Link Full Duplex estabelecido com a Terra.</div>
                </div>
            </div>

        </div>

    </main>

    <div id="infoModal" class="fixed inset-0 bg-space-950/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-space-900 border border-quantum-cyan/50 rounded-2xl max-w-2xl w-full p-6 space-y-4 glow-cyan relative max-h-[90vh] overflow-y-auto">
            <div class="flex items-center justify-between border-b border-space-800 pb-3">
                <h3 class="font-orbitron font-bold text-lg text-quantum-cyan flex items-center gap-2">
                    <i class="fa-solid fa-atom text-quantum-cyan"></i> Visão Geral do Aplicativo & Fundamentos
                </h3>
                <button onclick="closeModal()" class="text-slate-400 hover:text-white text-lg"><i class="fa-solid fa-xmark"></i></button>
            </div>
            
            <div class="space-y-3 text-xs text-slate-300 leading-relaxed">
                <p>
                    <strong class="text-quantum-cyan">Problema Resolvido:</strong> A crise energética global e a dependência insustentável de combustíveis fósseis ou baterias químicas limitadas são eliminadas através da captação de energia limpa e infinita diretamente no espaço.
                </p>
                <p>
                    <strong class="text-emerald-400">Extração do Vácuo Quântico:</strong> Naves automáticas em órbita terrestre utilizam rotores supercondutores em movimento circular de alta velocidade para excitar flutuações do vácuo quântico, convertendo energia de ponto zero em eletricidade pura.
                </p>
                <p>
                    <strong class="text-amber-400">Feixe Laser Full Duplex:</strong> O SROS transmite essa energia para a superfície do planeta através de uma corda de fótons perfeitamente alinhada. O sistema Full Duplex garante rastreamento bidirecional e compensação atmosférica em tempo real, eliminando a necessidade de cabos físicos.
                </p>
                <div class="bg-space-950 p-3 rounded-xl border border-space-800 space-y-1">
                    <div class="font-bold text-quantum-cyan">Recursos do Simulador:</div>
                    <ul class="list-disc pl-4 space-y-1 text-slate-400">
                        <li><strong>Visão Global Orbital:</strong> Planeta Terra com rotatividade e cidades iluminadas em tempo real.</li>
                        <li><strong>Rotor Quântico:</strong> Animação detalhada da extração de energia por partículas de vácuo.</li>
                        <li><strong>Controle de Gimbals:</strong> Ajustes dinâmicos de estabilidade e feixe laser.</li>
                    </ul>
                </div>
            </div>

            <div class="pt-3 border-t border-space-800 flex justify-end">
                <button onclick="closeModal()" class="px-4 py-2 rounded-xl bg-quantum-cyan text-space-950 font-bold text-xs hover:bg-emerald-400 transition-all glow-cyan">
                    Entendido, Iniciar Simulação
                </button>
            </div>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('simCanvas');
        const ctx = canvas.getContext('2d');

        let currentView = 'global'; // 'global', 'quantum', 'cities'
        let isRunning = true;
        let timeScale = 1;
        let simulationTime = 0;
        
        let rotorSpeedRPM = 7500;
        let autoAlignActive = true;
        let laserIntensity = 75;
        let interlockActive = false;

        let energyGeneratedGW = 4850;
        let transmissionEff = 99.4;
        let gridSaturation = 88.2;

        let particles = [];

        function resizeCanvas() {
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width * window.devicePixelRatio;
            canvas.height = rect.height * window.devicePixelRatio;
            ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        // --- AUDIO SYSTEM ---
        let audioCtx = null;
        let audioMuted = true;
        let ambientOsc = null;
        let ambientGain = null;

        function toggleAudio() {
            audioMuted = !audioMuted;
            const icon = document.getElementById('audio-icon');
            if (!audioMuted) {
                icon.className = "fa-solid fa-volume-high text-quantum-cyan";
                initWebAudio();
                addLog("Áudio ambiente quântico ativado.");
            } else {
                icon.className = "fa-solid fa-volume-xmark";
                if (audioCtx && audioCtx.state === 'running') {
                    audioCtx.suspend();
                }
                addLog("Áudio desativado.");
            }
        }

        function initWebAudio() {
            if (!audioCtx) {
                audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            }
            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }
            if (!ambientOsc) {
                ambientOsc = audioCtx.createOscillator();
                ambientGain = audioCtx.createGain();
                
                ambientOsc.type = 'triangle';
                ambientOsc.frequency.setValueAtTime(65, audioCtx.currentTime);
                ambientGain.gain.setValueAtTime(0.02, audioCtx.currentTime);

                ambientOsc.connect(ambientGain);
                ambientGain.connect(audioCtx.destination);
                ambientOsc.start();
            }
        }

        // --- VIEW SWITCHING ---
        function switchView(view) {
            currentView = view;
            ['global', 'quantum', 'cities'].forEach(v => {
                const btn = document.getElementById(`tab-${v}`);
                if (v === view) {
                    btn.className = "px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all bg-quantum-cyan/25 text-quantum-cyan border border-quantum-cyan/60 glow-cyan flex items-center gap-2";
                } else {
                    btn.className = "px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all text-slate-400 hover:text-quantum-cyan hover:bg-space-800 border border-transparent flex items-center gap-2";
                }
            });

            const titles = {
                global: "MODO: TRANSMISSÃO FULL DUPLEX ATIVA (ÓRBITA GLOBAL)",
                quantum: "MODO: ZOOM NO ROTOR DE VÁCUO QUÂNTICO SROS",
                cities: "MODO: DISTRIBUIÇÃO NAS CIDADES PLANETÁRIAS"
            };
            const descs = {
                global: "Naves SROS em órbita terrestre capturam energia limpa do vácuo quântico e transmitem via laser Full Duplex para as estações receptoras na superfície.",
                quantum: "Detalhe interno do rotor supercondutor girando a alta velocidade para extrair energia de ponto zero das flutuações do vácuo quântico.",
                cities: "As redes de distribuição sem fios alimentam centros urbanos globais com estabilidade e zero emissão de carbono."
            };
            document.getElementById('hud-title').innerText = titles[view];
            document.getElementById('view-desc').innerText = descs[view];
            addLog(`Alternado para a visualização: ${view.toUpperCase()}`);
        }

        // --- CONTROLS ---
        function togglePlayPause() {
            isRunning = !isRunning;
            const icon = document.getElementById('icon-play');
            const btn = document.getElementById('btn-play');
            if (isRunning) {
                icon.className = "fa-solid fa-pause";
                btn.classList.add('bg-quantum-cyan', 'glow-cyan');
                btn.classList.remove('bg-space-800');
                addLog("Simulação retomada.");
            } else {
                icon.className = "fa-solid fa-play";
                btn.classList.remove('bg-quantum-cyan', 'glow-cyan');
                btn.classList.add('bg-space-800');
                addLog("Simulação pausada.");
            }
        }

        function setSpeed(spd) {
            timeScale = spd;
            [1, 3, 5].forEach(s => {
                const b = document.getElementById(`spd-${s}`);
                if (s === spd) {
                    b.className = "px-2.5 py-1 rounded-lg text-xs font-bold bg-quantum-cyan/25 text-quantum-cyan border border-quantum-cyan";
                } else {
                    b.className = "px-2.5 py-1 rounded-lg text-xs font-bold bg-space-800 text-slate-400 border border-space-700";
                }
            });
            addLog(`Velocidade ajustada para ${spd}x.`);
        }

        function triggerEmergencyCutoff() {
            interlockActive = !interlockActive;
            const alertElem = document.getElementById('interlock-alert');
            if (interlockActive) {
                alertElem.classList.remove('hidden');
                addLog("ALERTA CRÍTICO: Interlock de emergência acionado! Feixe laser cortado.");
            } else {
                alertElem.classList.add('hidden');
                addLog("Interlock desativado. Reiniciando feixe laser Full Duplex.");
            }
        }

        function updateRotorSpeed(val) {
            rotorSpeedRPM = parseInt(val);
            document.getElementById('label-rotor').innerText = rotorSpeedRPM.toLocaleString() + " RPM";
            energyGeneratedGW = Math.round((rotorSpeedRPM / 10000) * 6500);
            document.getElementById('val-power').innerText = energyGeneratedGW.toLocaleString() + " GW";
            document.getElementById('bar-power').style.width = Math.min(100, (rotorSpeedRPM / 10000) * 100) + "%";
            addLog(`Velocidade do rotor ajustada para ${rotorSpeedRPM.toLocaleString()} RPM (${energyGeneratedGW} GW).`);
        }

        function toggleAutoAlign() {
            autoAlignActive = !autoAlignActive;
            const btn = document.getElementById('btn-align');
            if (autoAlignActive) {
                btn.innerText = "LIGADO";
                btn.className = "px-3 py-1 rounded-lg text-xs font-bold bg-emerald-500/20 text-emerald-400 border border-emerald-500/50 glow-emerald transition-all";
                transmissionEff = 99.4;
                document.getElementById('hud-align').innerText = "99.98% (Estável)";
                addLog("IA AutoNav & Gimbals magnéticos reativados.");
            } else {
                btn.innerText = "DESLIGADO";
                btn.className = "px-3 py-1 rounded-lg text-xs font-bold bg-space-800 text-slate-400 border border-space-700 transition-all";
                transmissionEff = 84.2;
                document.getElementById('hud-align').innerText = "84.2% (Oscilando)";
                addLog("ALERTA: Alinhamento automático desligado. Perda atmosférica aumentada!");
            }
            document.getElementById('val-eff').innerText = transmissionEff + "%";
            document.getElementById('bar-eff').style.width = transmissionEff + "%";
        }

        function updateLaserIntensity(val) {
            laserIntensity = parseInt(val);
            const labels = { 25: "Econômico (25%)", 50: "Moderado (50%)", 75: "Padrão (75%)", 100: "Overdrive (100%)" };
            document.getElementById('label-laser').innerText = labels[val] || (val + "%");
            addLog(`Intensidade do feixe laser ajustada para ${val}%.`);
        }

        function openModal() {
            document.getElementById('infoModal').classList.remove('hidden');
        }
        function closeModal() {
            document.getElementById('infoModal').classList.add('hidden');
        }

        function clearLogs() {
            document.getElementById('log-container').innerHTML = `<div class="text-slate-400">[Console limpo pelo operador]</div>`;
        }

        function addLog(text) {
            const container = document.getElementById('log-container');
            const now = new Date().toTimeString().split(' ')[0];
            const div = document.createElement('div');
            div.className = "text-slate-300";
            div.innerHTML = `<span class="text-quantum-cyan">[${now}]</span> ${text}`;
            container.appendChild(div);
            container.scrollTop = container.scrollHeight;
        }

        // --- DRAWING FUNCTIONS ---

        function drawStarfield(w, h) {
            ctx.fillStyle = '#020617';
            ctx.fillRect(0, 0, w, h);

            ctx.fillStyle = '#ffffff';
            for (let i = 0; i < 80; i++) {
                let x = (Math.sin(i * 77) * 10000) % w;
                let y = (Math.cos(i * 99) * 10000) % h;
                if (x < 0) x += w;
                if (y < 0) y += h;
                let alpha = 0.2 + (Math.sin(simulationTime * 0.05 + i) * 0.2);
                ctx.globalAlpha = Math.max(0.1, alpha);
                ctx.fillRect(x, y, 1.5, 1.5);
            }
            ctx.globalAlpha = 1.0;
        }

        // Global View (Earth + Orbiting SROS + Laser Rope)
        function drawGlobalView(w, h) {
            drawStarfield(w, h);
            const cx = w / 2;
            const cy = h / 2 + 30;
            const earthRadius = 110;

            // Draw Earth Atmosphere Glow
            const atmosGrad = ctx.createRadialGradient(cx, cy, earthRadius * 0.9, cx, cy, earthRadius * 1.3);
            atmosGrad.addColorStop(0, 'rgba(0, 243, 255, 0.25)');
            atmosGrad.addColorStop(1, 'transparent');
            ctx.fillStyle = atmosGrad;
            ctx.beginPath();
            ctx.arc(cx, cy, earthRadius * 1.3, 0, Math.PI * 2);
            ctx.fill();

            // Draw Earth Body
            const earthGrad = ctx.createRadialGradient(cx - 30, cy - 30, 20, cx, cy, earthRadius);
            earthGrad.addColorStop(0, '#38bdf8');
            earthGrad.addColorStop(0.6, '#0284c7');
            earthGrad.addColorStop(1, '#0f172a');
            ctx.fillStyle = earthGrad;
            ctx.beginPath();
            ctx.arc(cx, cy, earthRadius, 0, Math.PI * 2);
            ctx.fill();

            // Draw continents rotation representation
            ctx.save();
            ctx.beginPath();
            ctx.arc(cx, cy, earthRadius, 0, Math.PI * 2);
            ctx.clip();
            ctx.fillStyle = '#10b981';
            let rotOffset = (simulationTime * 0.005) % (Math.PI * 2);
            for (let i = 0; i < 5; i++) {
                let px = cx + Math.sin(i + rotOffset) * 60;
                let py = cy + Math.cos(i * 1.5 + rotOffset) * 50;
                ctx.beginPath();
                ctx.arc(px, py, 28, 0, Math.PI * 2);
                ctx.fill();
            }
            ctx.restore();

            // Ground Station on Earth (top surface)
            let groundX = cx;
            let groundY = cy - earthRadius;
            ctx.fillStyle = '#f59e0b';
            ctx.beginPath();
            ctx.arc(groundX, groundY, 4, 0, Math.PI * 2);
            ctx.fill();

            // Orbital SROS Spacecraft position
            let orbitAngle = simulationTime * 0.015;
            let orbitRadiusDist = earthRadius + 95;
            let srosX = cx + Math.cos(orbitAngle - Math.PI/2) * 20;
            let srosY = cy - orbitRadiusDist;

            // Draw Full Duplex Laser "Rope" if interlock is off
            if (!interlockActive) {
                const laserWidth = (laserIntensity / 100) * 4 + 1;
                const laserGrad = ctx.createLinearGradient(srosX, srosY, groundX, groundY);
                laserGrad.addColorStop(0, 'rgba(0, 243, 255, 0.9)');
                laserGrad.addColorStop(0.5, 'rgba(16, 185, 129, 0.8)');
                laserGrad.addColorStop(1, 'rgba(245, 158, 11, 0.9)');

                ctx.strokeStyle = laserGrad;
                ctx.lineWidth = laserWidth;
                ctx.beginPath();
                ctx.moveTo(srosX, srosY);
                ctx.lineTo(groundX, groundY);
                ctx.stroke();

                // Animated Photon Energy Particles flowing along the laser rope
                if (isRunning) {
                    for (let i = 0; i < 3; i++) {
                        let tFactor = ((simulationTime * 0.03 + i * 0.33) % 1.0);
                        let px = srosX + (groundX - srosX) * tFactor;
                        let py = srosY + (groundY - srosY) * tFactor;
                        ctx.fillStyle = '#ffffff';
                        ctx.beginPath();
                        ctx.arc(px, py, 2.5, 0, Math.PI * 2);
                        ctx.fill();
                    }
                }
            }

            // Draw SROS Orbital Station
            ctx.save();
            ctx.translate(srosX, srosY);
            ctx.rotate(simulationTime * 0.05);

            // Rotating Quantum Vacuum Ring
            ctx.strokeStyle = '#00f3ff';
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.arc(0, 0, 22, 0, Math.PI * 2);
            ctx.stroke();

            // Station Core
            ctx.fillStyle = '#1e293b';
            ctx.strokeStyle = '#10b981';
            ctx.lineWidth = 2;
            ctx.fillRect(-12, -12, 24, 24);
            ctx.strokeRect(-12, -12, 24, 24);

            ctx.restore();

            // Label SROS
            ctx.fillStyle = '#00f3ff';
            ctx.font = '10px JetBrains Mono';
            ctx.fillText("SROS-QUANTUM #01", srosX + 28, srosY + 4);
        }

        // Quantum View (Zoom into Rotor)
        function drawQuantumView(w, h) {
            drawStarfield(w, h);
            const cx = w / 2;
            const cy = h / 2;

            // Outer Vacuum Chamber
            ctx.strokeStyle = 'rgba(0, 243, 255, 0.3)';
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.arc(cx, cy, 140, 0, Math.PI * 2);
            ctx.stroke();

            // Rotating Superconducting Rings
            ctx.save();
            ctx.translate(cx, cy);
            let spinAngle = simulationTime * (rotorSpeedRPM / 2000) * timeScale;
            ctx.rotate(spinAngle);

            ctx.strokeStyle = '#10b981';
            ctx.lineWidth = 8;
            ctx.beginPath();
            ctx.arc(0, 0, 90, 0, Math.PI * 1.5);
            ctx.stroke();

            ctx.strokeStyle = '#00f3ff';
            ctx.lineWidth = 6;
            ctx.beginPath();
            ctx.arc(0, 0, 60, Math.PI, Math.PI * 2.5);
            ctx.stroke();

            // Quantum Vortex Particles
            ctx.fillStyle = '#ffffff';
            for (let i = 0; i < 12; i++) {
                let angle = (i / 12) * Math.PI * 2 + spinAngle;
                let px = Math.cos(angle) * 75;
                let py = Math.sin(angle) * 75;
                ctx.beginPath();
                ctx.arc(px, py, 3, 0, Math.PI * 2);
                ctx.fill();
            }

            ctx.restore();

            // Center Core Energy Pulse
            const coreGrad = ctx.createRadialGradient(cx, cy, 5, cx, cy, 35);
            coreGrad.addColorStop(0, '#ffffff');
            coreGrad.addColorStop(0.5, '#00f3ff');
            coreGrad.addColorStop(1, 'transparent');
            ctx.fillStyle = coreGrad;
            ctx.beginPath();
            ctx.arc(cx, cy, 35, 0, Math.PI * 2);
            ctx.fill();

            // Overlay Text
            ctx.fillStyle = '#00f3ff';
            ctx.font = '12px Orbitron';
            ctx.fillText(`ROTATOR RPM: ${rotorSpeedRPM.toLocaleString()}`, cx - 110, cy + 170);
            ctx.fillStyle = '#10b981';
            ctx.font = '11px JetBrains Mono';
            ctx.fillText(`EXTRAÇÃO DE PONTO ZERO: ${energyGeneratedGW} GW`, cx - 130, cy + 190);
        }

        // Cities View (Global Power Distribution)
        function drawCitiesView(w, h) {
            drawStarfield(w, h);
            const cx = w / 2;
            const cy = h / 2;

            // Draw curved Earth horizon at bottom
            ctx.fillStyle = '#0f172a';
            ctx.beginPath();
            ctx.arc(cx, cy + 300, 320, 0, Math.PI * 2);
            ctx.fill();

            ctx.strokeStyle = '#00f3ff';
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.arc(cx, cy + 300, 320, Math.PI, Math.PI * 2);
            ctx.stroke();

            // Draw interconnected cities with power nodes
            const cities = [
                { name: "Nova Tóquio", x: cx - 180, y: cy + 40, power: "1,250 GW" },
                { name: "São Paulo Prime", x: cx, y: cy + 20, power: "980 GW" },
                { name: "Nova Alexandria", x: cx + 180, y: cy + 50, power: "1,420 GW" }
            ];

            cities.forEach((city, idx) => {
                // City tower representation
                ctx.fillStyle = '#38bdf8';
                ctx.fillRect(city.x - 10, city.y - 25, 20, 30);

                // Glowing energy dome
                ctx.fillStyle = 'rgba(16, 185, 129, 0.3)';
                ctx.beginPath();
                ctx.arc(city.x, city.y - 25, 18, 0, Math.PI * 2);
                ctx.fill();

                // Beam from orbital relay to city
                ctx.strokeStyle = 'rgba(0, 243, 255, 0.6)';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.moveTo(city.x, city.y - 43);
                ctx.lineTo(city.x, cy - 120);
                ctx.stroke();

                // City label
                ctx.fillStyle = '#ffffff';
                ctx.font = '11px JetBrains Mono';
                ctx.fillText(city.name, city.x - 40, city.y + 20);
                ctx.fillStyle = '#10b981';
                ctx.fillText(city.power, city.x - 32, city.y + 34);
            });

            // Orbital relay node
            ctx.fillStyle = '#00f3ff';
            ctx.beginPath();
            ctx.arc(cx, cy - 120, 6, 0, Math.PI * 2);
            ctx.fill();
            ctx.fillStyle = '#00f3ff';
            ctx.font = '10px Orbitron';
            ctx.fillText("SROS CENTRAL RELAY NODE", cx - 85, cy - 135);
        }

        // Main Animation Loop
        function simulationLoop() {
            const w = canvas.clientWidth;
            const h = canvas.clientHeight;

            if (canvas.width !== w * window.devicePixelRatio || canvas.height !== h * window.devicePixelRatio) {
                canvas.width = w * window.devicePixelRatio;
                canvas.height = h * window.devicePixelRatio;
                ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
            }

            ctx.clearRect(0, 0, w, h);

            if (isRunning) {
                simulationTime += 1 * timeScale;
            }

            if (currentView === 'global') {
                drawGlobalView(w, h);
            } else if (currentView === 'quantum') {
                drawQuantumView(w, h);
            } else if (currentView === 'cities') {
                drawCitiesView(w, h);
            }

            requestAnimationFrame(simulationLoop);
        }

        window.onload = function() {
            addLog("Sistema SROS Power Grid online. Transmissão sem fios ativa.");
            requestAnimationFrame(simulationLoop);
        };
    </script>
</body>
</html>
