<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>French Hoops Hub - The Golden Generation</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;600;800&family=Playfair+Display:ital,wght@1,700&display=swap" rel="stylesheet">
    
    <style>
        body { font-family: 'Montserrat', sans-serif; background-color: #f8fafc; }
        h1, h2, h3, .font-serif { font-family: 'Playfair Display', serif; }
        
        /* Barwy Francji */
        .text-bleu { color: #002395; }
        .bg-bleu { background-color: #002395; }
        .text-rouge { color: #ED2939; }
        .bg-rouge { background-color: #ED2939; }
        
        /* Efekty */
        .glass-card {
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .hero-gradient {
            background: linear-gradient(135deg, #002395 0%, #0a192f 100%);
        }
        
        /* Czat */
        .chat-container::-webkit-scrollbar { width: 6px; }
        .chat-container::-webkit-scrollbar-track { background: #f1f1f1; }
        .chat-container::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        
        /* Animacja pisania */
        .typing-dot {
            animation: typing 1.4s infinite ease-in-out both;
        }
        .typing-dot:nth-child(1) { animation-delay: -0.32s; }
        .typing-dot:nth-child(2) { animation-delay: -0.16s; }
        
        @keyframes typing {
            0%, 80%, 100% { transform: scale(0); }
            40% { transform: scale(1); }
        }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        const { useState, useEffect, useRef } = React;

        // --- BAZA WIEDZY I DANE ---
        const PLAYERS = [
            {
                id: 1,
                name: "Victor Wembanyama",
                nickname: "L'Alien",
                img: "https://images.unsplash.com/photo-1519766304800-c95190085667?q=80&w=800&auto=format&fit=crop", // Symboliczne zdjęcie
                desc: "Rewolucja w ludzkiej postaci. 224 cm wzrostu, ruchy rozgrywającego. Rookie of the Year 2024.",
                stats: "21.4 PPG | 10.6 RPG | 3.6 BPG"
            },
            {
                id: 2,
                name: "Tony Parker",
                nickname: "TP9",
                img: "https://images.unsplash.com/photo-1505666287802-931dc83948e9?q=80&w=800&auto=format&fit=crop",
                desc: "Ojciec chrzestny francuskiego basketu. 4 pierścienie NBA ze Spurs. Pierwszy europejski MVP Finałów.",
                stats: "Hall of Fame | 4x NBA Champ"
            },
            {
                id: 3,
                name: "Rudy Gobert",
                nickname: "Stifle Tower",
                img: "https://images.unsplash.com/photo-1628779238951-bd5c9e7a5e8c?q=80&w=800&auto=format&fit=crop",
                desc: "Minister Obrony Narodowej. Czterokrotny zdobywca nagrody dla najlepszego obrońcy NBA (DPOY).",
                stats: "4x DPOY | 3x All-Star"
            }
        ];

        // Symulowana sztuczna inteligencja (działa bez klucza API!)
        const AI_KNOWLEDGE = {
            "wembanyama": "Victor Wembanyama to fenomen. Nazywany 'Alien' przez LeBrona Jamesa. Jest nadzieją Spurs i kadry Francji na złoto w Los Angeles 2028.",
            "parker": "Tony Parker to legenda. Jego manewr 'spin move' był nie do zatrzymania. Obecnie jest właścicielem klubu ASVEL Lyon-Villeurbanne.",
            "gobert": "Rudy Gobert to defensywna kotwica. Choć bywa krytykowany za ofensywę, jego wpływ na obronę jest historyczny.",
            "francja": "Reprezentacja Francji to obecni wicemistrzowie olimpijscy (Paryż 2024). Mają niesamowity system szkolenia w INSEP.",
            "nba": "W NBA gra obecnie rekordowa liczba Francuzów, w tym Sarr, Risacher i oczywiście Wemby. Francja to druga siła w NBA po USA.",
            "default": "To ciekawe pytanie! Francuska koszykówka przeżywa Złotą Erę. Zapytaj mnie o Parkera, Wembanyamę, Goberta lub kadrę narodową!"
        };

        const Navbar = () => (
            <nav className="fixed w-full z-50 bg-white/90 backdrop-blur-md border-b border-gray-100 shadow-sm">
                <div className="max-w-7xl mx-auto px-6 h-20 flex justify-between items-center">
                    <div className="text-2xl font-serif font-bold tracking-tighter">
                        FRENCH<span className="text-bleu">HOOPS</span><span className="text-rouge">.HUB</span>
                    </div>
                    <div className="hidden md:flex space-x-8 text-sm font-semibold tracking-wide text-gray-600">
                        <a href="#hero" className="hover:text-bleu transition">START</a>
                        <a href="#legends" className="hover:text-bleu transition">IKONY</a>
                        <a href="#facts" className="hover:text-bleu transition">CIEKAWOSTKI</a>
                        <a href="#ai-assistant" className="px-4 py-2 bg-bleu text-white rounded-full hover:bg-blue-800 transition shadow-lg shadow-blue-900/20">CHAT AI</a>
                    </div>
                </div>
            </nav>
        );

        const Hero = () => (
            <section id="hero" className="relative pt-32 pb-20 lg:pt-48 lg:pb-32 overflow-hidden bg-gray-50">
                <div className="absolute top-0 right-0 w-1/2 h-full bg-blue-50/50 skew-x-12 transform origin-top-right"></div>
                <div className="max-w-7xl mx-auto px-6 relative z-10 grid lg:grid-cols-2 gap-12 items-center">
                    <div className="space-y-8">
                        <span className="inline-block px-4 py-1.5 bg-rouge/10 text-rouge font-bold text-xs tracking-widest rounded-full uppercase">
                            La Révolution est arrivée
                        </span>
                        <h1 className="text-5xl lg:text-7xl font-serif font-bold text-gray-900 leading-[1.1]">
                            Od Parkera <br/> do <span className="text-transparent bg-clip-text bg-gradient-to-r from-bleu to-rouge">Wembanyamy</span>
                        </h1>
                        <p className="text-lg text-gray-600 leading-relaxed max-w-lg">
                            Francja stała się drugą potęgą koszykarską świata. Poznaj historię, statystyki i przyszłość "Les Bleus" na interaktywnej platformie.
                        </p>
                        <div className="flex gap-4">
                            <a href="#ai-assistant" className="group px-8 py-4 bg-gray-900 text-white rounded-xl font-semibold shadow-xl hover:shadow-2xl hover:-translate-y-1 transition duration-300 flex items-center gap-2">
                                Zapytaj Eksperta AI 
                                <span>→</span>
                            </a>
                        </div>
                    </div>
                    <div className="relative">
                        <div className="absolute inset-0 bg-gradient-to-tr from-bleu to-rouge rounded-[2rem] blur-2xl opacity-20 transform rotate-6"></div>
                        <img 
                            src="https://images.unsplash.com/photo-1546519638-68e109498ffc?q=80&w=1000&auto=format&fit=crop" 
                            alt="Basketball Art" 
                            className="relative rounded-[2rem] shadow-2xl border-4 border-white rotate-[-3deg] hover:rotate-0 transition duration-500 object-cover h-[500px] w-full"
                        />
                    </div>
                </div>
            </section>
        );

        const Legends = () => (
            <section id="legends" className="py-24 bg-white">
                <div className="max-w-7xl mx-auto px-6">
                    <div className="text-center mb-16">
                        <h2 className="text-4xl font-serif font-bold mb-4">Ikony Francuskiego Basketu</h2>
                        <div className="w-20 h-1 bg-bleu mx-auto rounded-full"></div>
                    </div>
                    <div className="grid md:grid-cols-3 gap-8">
                        {PLAYERS.map((player) => (
                            <div key={player.id} className="group relative bg-white rounded-2xl shadow-lg border border-gray-100 overflow-hidden hover:shadow-2xl transition duration-300">
                                <div className="h-64 overflow-hidden">
                                    <img src={player.img} alt={player.name} className="w-full h-full object-cover group-hover:scale-110 transition duration-700" />
                                    <div className="absolute top-4 right-4 bg-white/90 backdrop-blur px-3 py-1 rounded-lg text-xs font-bold shadow-sm">
                                        {player.nickname}
                                    </div>
                                </div>
                                <div className="p-8">
                                    <h3 className="text-2xl font-serif font-bold text-gray-900 mb-2">{player.name}</h3>
                                    <p className="text-bleu font-semibold text-sm mb-4">{player.stats}</p>
                                    <p className="text-gray-600 text-sm leading-relaxed">{player.desc}</p>
                                </div>
                                <div className="absolute bottom-0 left-0 w-full h-1 bg-gradient-to-r from-bleu via-white to-rouge transform scale-x-0 group-hover:scale-x-100 transition duration-500"></div>
                            </div>
                        ))}
                    </div>
                </div>
            </section>
        );

        const Facts = () => (
            <section id="facts" className="py-20 bg-gray-900 text-white overflow-hidden relative">
                <div className="absolute inset-0 opacity-10" style={{backgroundImage: 'radial-gradient(#444 1px, transparent 1px)', backgroundSize: '20px 20px'}}></div>
                <div className="max-w-7xl mx-auto px-6 relative z-10">
                    <div className="grid md:grid-cols-2 gap-16 items-center">
                        <div>
                            <h2 className="text-3xl md:text-5xl font-serif font-bold mb-6">Czy wiesz, że...</h2>
                            <div className="space-y-6">
                                <div className="flex gap-4">
                                    <div className="w-12 h-12 rounded-full bg-bleu flex items-center justify-center font-bold text-xl flex-shrink-0">1</div>
                                    <p className="text-gray-300">Pierwszy mecz koszykówki w Europie rozegrano w Paryżu w 1893 roku, zaledwie dwa lata po wynalezieniu gry przez Naismitha.</p>
                                </div>
                                <div className="flex gap-4">
                                    <div className="w-12 h-12 rounded-full bg-white text-gray-900 flex items-center justify-center font-bold text-xl flex-shrink-0">2</div>
                                    <p className="text-gray-300">Francja jest jedynym krajem, który dwukrotnie z rzędu grał z USA w finale Igrzysk Olimpijskich (2020, 2024).</p>
                                </div>
                                <div className="flex gap-4">
                                    <div className="w-12 h-12 rounded-full bg-rouge flex items-center justify-center font-bold text-xl flex-shrink-0">3</div>
                                    <p className="text-gray-300">Betonowe boiska w Paryżu (np. Pigalle Duperré) są uznawane za najpiękniejsze artystyczne boiska na świecie.</p>
                                </div>
                            </div>
                        </div>
                        <div className="bg-gradient-to-br from-bleu to-blue-900 p-8 rounded-3xl shadow-2xl transform rotate-2 hover:rotate-0 transition duration-500">
                            <h3 className="text-2xl font-bold mb-2">Słowo od twórcy</h3>
                            <p className="opacity-80 italic mb-6">"Ten projekt to hołd dla ewolucji francuskiego basketu. Od ulic Paryża po parkiety NBA."</p>
                            <div className="flex items-center gap-4">
                                <div className="w-10 h-10 bg-white rounded-full"></div>
                                <div>
                                    <p className="font-bold text-sm">Twój GitHub</p>
                                    <p className="text-xs opacity-70">Frontend Developer & Basket Fan</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </section>
        );

        const AIAssistant = () => {
            const [messages, setMessages] = useState([
                { type: 'bot', text: 'Bonjour! Jestem ekspertem od francuskiej koszykówki. Zapytaj mnie o Wembanyamę, Parkera, Goberta lub historię kadry!' }
            ]);
            const [input, setInput] = useState('');
            const [isTyping, setIsTyping] = useState(false);
            const messagesEndRef = useRef(null);

            const scrollToBottom = () => {
                messagesEndRef.current?.scrollIntoView({ behavior: "smooth" });
            };

            useEffect(scrollToBottom, [messages, isTyping]);

            const handleSend = (e) => {
                e.preventDefault();
                if (!input.trim()) return;

                const userText = input;
                setMessages(prev => [...prev, { type: 'user', text: userText }]);
                setInput('');
                setIsTyping(true);

                // Symulacja myślenia AI
                setTimeout(() => {
                    const lowerText = userText.toLowerCase();
                    let response = AI_KNOWLEDGE['default'];
                    
                    if (lowerText.includes('wemby') || lowerText.includes('wembanyama') || lowerText.includes('alien')) response = AI_KNOWLEDGE['wembanyama'];
                    else if (lowerText.includes('parker') || lowerText.includes('tony')) response = AI_KNOWLEDGE['parker'];
                    else if (lowerText.includes('gobert') || lowerText.includes('rudy')) response = AI_KNOWLEDGE['gobert'];
                    else if (lowerText.includes('francja') || lowerText.includes('kadra') || lowerText.includes('igrzyska')) response = AI_KNOWLEDGE['francja'];
                    else if (lowerText.includes('nba') || lowerText.includes('draft')) response = AI_KNOWLEDGE['nba'];

                    setMessages(prev => [...prev, { type: 'bot', text: response }]);
                    setIsTyping(false);
                }, 1500);
            };

            return (
                <section id="ai-assistant" className="py-24 bg-blue-50">
                    <div className="max-w-3xl mx-auto px-6">
                        <div className="bg-white rounded-2xl shadow-xl overflow-hidden border border-blue-100 flex flex-col h-[600px]">
                            <div className="bg-bleu p-6 text-white flex justify-between items-center">
                                <div>
                                    <h3 className="font-bold text-lg">Wirtualny Ekspert LNB</h3>
                                    <p className="text-xs text-blue-200">Powered by Simulated Intelligence</p>
                                </div>
                                <div className="w-3 h-3 bg-green-400 rounded-full shadow-[0_0_10px_#4ade80]"></div>
                            </div>
                            
                            <div className="flex-1 p-6 overflow-y-auto chat-container bg-slate-50 space-y-4">
                                {messages.map((msg, idx) => (
                                    <div key={idx} className={`flex ${msg.type === 'user' ? 'justify-end' : 'justify-start'}`}>
                                        <div className={`max-w-[80%] p-4 rounded-2xl text-sm leading-relaxed ${
                                            msg.type === 'user' 
                                            ? 'bg-bleu text-white rounded-br-none shadow-md' 
                                            : 'bg-white text-gray-800 rounded-bl-none shadow-sm border border-gray-100'
                                        }`}>
                                            {msg.text}
                                        </div>
                                    </div>
                                ))}
                                {isTyping && (
                                    <div className="flex justify-start">
                                        <div className="bg-white p-4 rounded-2xl rounded-bl-none shadow-sm border border-gray-100 flex gap-1">
                                            <div className="w-2 h-2 bg-gray-400 rounded-full typing-dot"></div>
                                            <div className="w-2 h-2 bg-gray-400 rounded-full typing-dot"></div>
                                            <div className="w-2 h-2 bg-gray-400 rounded-full typing-dot"></div>
                                        </div>
                                    </div>
                                )}
                                <div ref={messagesEndRef} />
                            </div>

                            <form onSubmit={handleSend} className="p-4 bg-white border-t border-gray-100 flex gap-3">
                                <input 
                                    type="text" 
                                    value={input}
                                    onChange={(e) => setInput(e.target.value)}
                                    placeholder="Napisz np. 'Kim jest Wembanyama?'..." 
                                    className="flex-1 bg-gray-100 text-gray-900 placeholder-gray-500 px-6 py-3 rounded-xl focus:outline-none focus:ring-2 focus:ring-bleu/50 transition"
                                />
                                <button type="submit" className="bg-rouge text-white px-6 py-3 rounded-xl font-bold hover:bg-red-700 transition shadow-lg shadow-red-500/30">
                                    Wyślij
                                </button>
                            </form>
                        </div>
                    </div>
                </section>
            );
        };

        const Footer = () => (
            <footer className="bg-gray-900 text-white py-12 border-t-4 border-bleu">
                <div className="max-w-7xl mx-auto px-6 text-center">
                    <h2 className="text-3xl font-serif font-bold mb-6">FRENCH<span className="text-rouge">HOOPS</span></h2>
                    <p className="text-gray-500 text-sm mb-8">© 2026 Projekt Edukacyjny. Wszystkie zdjęcia użyte w celach demonstracyjnych.</p>
                    <div className="flex justify-center gap-6">
                        <div className="w-12 h-1 bg-bleu rounded-full"></div>
                        <div className="w-12 h-1 bg-white rounded-full"></div>
                        <div className="w-12 h-1 bg-rouge rounded-full"></div>
                    </div>
                </div>
            </footer>
        );

        const App = () => (
            <div className="min-h-screen flex flex-col">
                <Navbar />
                <Hero />
                <Legends />
                <Facts />
                <AIAssistant />
                <Footer />
            </div>
        );

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>
</html>
