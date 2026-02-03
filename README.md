<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Francuska Koszykówka - Golden Era</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://unpkg.com/recharts/umd/Recharts.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&family=Oswald:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; scroll-behavior: smooth; }
        h1, h2, h3, .font-oswald { font-family: 'Oswald', sans-serif; }
        .bg-bleu-de-france { background-color: #002395; }
        .text-bleu-de-france { color: #002395; }
        .border-bleu-de-france { border-color: #002395; }
        .bg-rouge-france { background-color: #ED2939; }
        .chat-scroll::-webkit-scrollbar { width: 6px; }
        .chat-scroll::-webkit-scrollbar-track { background: #f1f1f1; }
        .chat-scroll::-webkit-scrollbar-thumb { background: #002395; border-radius: 10px; }
    </style>
</head>
<body class="bg-gray-50 text-gray-900">
    <div id="root"></div>

    <script type="text/babel">
        const { useState, useRef, useEffect } = React;
        const { AreaChart, Area, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer } = Recharts;

        // --- DANE ---
        const PLAYERS = [
          {
            id: 'wemby',
            name: 'Victor Wembanyama',
            team: 'San Antonio Spurs',
            position: 'Center/Power Forward',
            image: 'https://images.unsplash.com/photo-1546519638-68e109498ffc?q=80&w=800&auto=format&fit=crop',
            description: 'Nazywany "Alienem", Wembanyama to największy talent w historii francuskiej koszykówki. Wybrany z numerem 1 w drafcie NBA 2023.',
            achievements: ['NBA Rookie of the Year 2024', 'Wicemistrz Olimpijski 2024', 'Lider bloków NBA']
          },
          {
            id: 'gobert',
            name: 'Rudy Gobert',
            team: 'Minnesota Timberwolves',
            position: 'Center',
            image: 'https://images.unsplash.com/photo-1519861531473-9200362f46b3?q=80&w=800&auto=format&fit=crop',
            description: '"The Stifle Tower" to filar defensywy reprezentacji Francji i wielokrotny najlepszy obrońca ligi NBA.',
            achievements: ['4x NBA Defensive Player of the Year', '3x NBA All-Star', 'Wicemistrz Olimpijski 2020, 2024']
          },
          {
            id: 'parker',
            name: 'Tony Parker',
            team: 'Legend (San Antonio Spurs)',
            position: 'Point Guard',
            image: 'https://images.unsplash.com/photo-1504450758481-7338eba7524a?q=80&w=800&auto=format&fit=crop',
            description: 'Najbardziej utytułowany francuski koszykarz w historii. Członek Hall of Fame i legenda Spurs.',
            achievements: ['4x Mistrz NBA', 'NBA Finals MVP 2007', 'Mistrz Europy 2013']
          }
        ];

        const NBA_GROWTH_DATA = [
          { year: 1997, count: 1 }, { year: 2001, count: 2 }, { year: 2005, count: 5 },
          { year: 2010, count: 8 }, { year: 2015, count: 10 }, { year: 2020, count: 12 }, { year: 2024, count: 14 }
        ];

        // --- KOMPONENTY ---
        const Navbar = () => (
          <nav className="sticky top-0 z-50 bg-white shadow-md border-b-4 border-bleu-de-france">
            <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
              <div className="flex justify-between h-20 items-center">
                <div className="flex items-center space-x-2">
                  <div className="w-10 h-10 bg-bleu-de-france flex items-center justify-center rounded-full text-white font-bold">FR</div>
                  <span className="text-2xl font-oswald font-bold tracking-tight">FRENCH<span className="text-rouge-france">HOOPS</span></span>
                </div>
                <div className="hidden md:flex space-x-8 font-semibold uppercase text-sm">
                  <a href="#hero" className="hover:text-bleu-de-france transition">Start</a>
                  <a href="#stars" className="hover:text-bleu-de-france transition">Gwiazdy</a>
                  <a href="#stats" className="hover:text-bleu-de-france transition">Rozwój</a>
                  <a href="#ai" className="hover:text-bleu-de-france transition">Ekspert AI</a>
                </div>
              </div>
            </div>
          </nav>
        );

        const Hero = () => (
          <section id="hero" className="relative h-[80vh] flex items-center overflow-hidden bg-black text-white">
            <div className="absolute inset-0 opacity-60">
              <img src="https://images.unsplash.com/photo-1544919982-b61976f0ba43?q=80&w=1920&auto=format&fit=crop" className="w-full h-full object-cover" />
            </div>
            <div className="absolute inset-0 bg-gradient-to-r from-black via-black/40 to-transparent"></div>
            <div className="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
              <div className="max-w-2xl">
                <span className="inline-block px-3 py-1 mb-4 text-sm font-bold tracking-widest bg-rouge-france rounded uppercase">La Nouvelle Ère</span>
                <h1 className="text-6xl md:text-8xl font-oswald font-bold leading-tight mb-6 uppercase">Złota Era <br/> <span className="text-bleu-de-france bg-white px-2">Francuskiego</span> Basketu</h1>
                <p className="text-xl md:text-2xl font-light mb-8 text-gray-300">Od legendy Tony'ego Parkera po fenomen Victora Wembanyamy. Odkryj potęgę "Les Bleus".</p>
                <div className="flex space-x-4">
                  <a href="#stars" className="px-8 py-4 bg-bleu-de-france text-white font-bold rounded-lg hover:bg-blue-700 transition transform hover:-translate-y-1">Poznaj Gwiazdy</a>
                  <a href="#ai" className="px-8 py-4 bg-white text-black font-bold rounded-lg hover:bg-gray-200 transition transform hover:-translate-y-1">Zapytaj AI</a>
                </div>
              </div>
            </div>
          </section>
        );

        const InfoCards = () => (
          <section className="py-20 bg-gray-50 border-b">
            <div className="max-w-7xl mx-auto px-4 grid grid-cols-1 md:grid-cols-3 gap-8">
              <div className="bg-white p-8 rounded-xl shadow-sm text-center border-t-4 border-bleu-de-france">
                <div className="text-4xl mb-4">🏅</div>
                <h4 className="font-bold mb-2 uppercase tracking-tight text-lg">Potęga Olimpijska</h4>
                <p className="text-sm text-gray-500">Srebrni medaliści z Tokio 2020 i Paryża 2024. Drużyna, która rzuca wyzwanie USA.</p>
              </div>
              <div className="bg-white p-8 rounded-xl shadow-sm text-center border-t-4 border-white">
                <div className="text-4xl mb-4">💎</div>
                <h4 className="font-bold mb-2 uppercase tracking-tight text-lg">Akademia Talentów</h4>
                <p className="text-sm text-gray-500">Słynny INSEP kształtujący najlepszych atletów Europy od dziesięcioleci.</p>
              </div>
              <div className="bg-white p-8 rounded-xl shadow-sm text-center border-t-4 border-rouge-france">
                <div className="text-4xl mb-4">📈</div>
                <h4 className="font-bold mb-2 uppercase tracking-tight text-lg">NBA Dominacja</h4>
                <p className="text-sm text-gray-500">Najwięcej graczy spoza USA w ostatnich draftach pochodzi właśnie z Francji.</p>
              </div>
            </div>
          </section>
        );

        const StatsSection = () => (
          <section id="stats" className="py-24 bg-gray-900 text-white overflow-hidden">
            <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
              <div className="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
                <div>
                  <h2 className="text-4xl md:text-5xl font-oswald font-bold mb-6 uppercase">Ekspansja do NBA</h2>
                  <div className="w-20 h-1 bg-bleu-de-france mb-8"></div>
                  <p className="text-gray-400 text-lg mb-6">Francja dostarcza największą liczbę zawodników do NBA spoza Ameryki Północnej. Zobacz dynamikę wzrostu na przestrzeni lat.</p>
                  <div className="grid grid-cols-2 gap-8 mt-12">
                    <div className="border-l-4 border-rouge-france pl-4">
                      <span className="block text-4xl font-oswald font-bold">14</span>
                      <span className="text-gray-400 uppercase text-sm">Aktywnych graczy</span>
                    </div>
                    <div className="border-l-4 border-bleu-de-france pl-4">
                      <span className="block text-4xl font-oswald font-bold">#1</span>
                      <span className="text-gray-400 uppercase text-sm">Draft 2024 Power</span>
                    </div>
                  </div>
                </div>
                <div className="bg-white/5 p-8 rounded-3xl border border-white/10 h-[400px]">
                  <ResponsiveContainer width="100%" height="100%">
                    <AreaChart data={NBA_GROWTH_DATA}>
                      <defs>
                        <linearGradient id="colorCount" x1="0" y1="0" x2="0" y2="1">
                          <stop offset="5%" stopColor="#002395" stopOpacity={0.8}/>
                          <stop offset="95%" stopColor="#002395" stopOpacity={0}/>
                        </linearGradient>
                      </defs>
                      <CartesianGrid strokeDasharray="3 3" stroke="#333" />
                      <XAxis dataKey="year" stroke="#888" />
                      <YAxis stroke="#888" />
                      <Tooltip contentStyle={{ backgroundColor: '#111', border: 'none', borderRadius: '10px' }} />
                      <Area type="monotone" dataKey="count" stroke="#002395" fill="url(#colorCount)" strokeWidth={3} />
                    </AreaChart>
                  </ResponsiveContainer>
                </div>
              </div>
            </div>
          </section>
        );

        const AIAnalyst = () => {
          const [messages, setMessages] = useState([
            { role: 'model', text: 'Witaj! Jestem Twoim ekspertem od francuskiej koszykówki. O co chcesz zapytać?' }
          ]);
          const [input, setInput] = useState('');
          const scrollRef = useRef(null);

          useEffect(() => {
            if (scrollRef.current) scrollRef.current.scrollTop = scrollRef.current.scrollHeight;
          }, [messages]);

          const handleSubmit = (e) => {
            e.preventDefault();
            if (!input.trim()) return;
            
            const userMsg = input;
            setInput('');
            setMessages(prev => [...prev, { role: 'user', text: userMsg }]);
            
            // Symulacja odpowiedzi (AI wymaga bezpiecznego klucza API, którego nie publikujemy na GitHubie)
            setTimeout(() => {
              setMessages(prev => [...prev, { 
                role: 'model', 
                text: `Analizuję Twoje pytanie o "${userMsg}". Francuski basket jest obecnie w najlepszym momencie w historii, dzięki systemowi szkolenia INSEP i nowej fali talentów w NBA!` 
              }]);
            }, 1000);
          };

          return (
            <section id="ai" className="py-24 bg-white">
              <div className="max-w-4xl mx-auto px-4">
                <div className="text-center mb-12">
                  <h2 className="text-4xl font-oswald font-bold mb-4 uppercase">Ekspert AI Francuskiego Basketu</h2>
                  <p className="text-gray-600">Zapytaj o statystyki, historię lub przyszłość talentów znad Sekwany.</p>
                </div>
                <div className="bg-white rounded-3xl shadow-2xl overflow-hidden flex flex-col h-[500px] border border-gray-100">
                  <div className="bg-bleu-de-france p-4 text-white flex items-center justify-between">
                    <span className="font-bold tracking-widest text-sm uppercase">Analyst FR-AI</span>
                    <div className="w-3 h-3 bg-green-400 rounded-full animate-pulse"></div>
                  </div>
                  <div ref={scrollRef} className="flex-1 p-6 overflow-y-auto space-y-4 chat-scroll bg-gray-50">
                    {messages.map((m, i) => (
                      <div key={i} className={`flex ${m.role === 'user' ? 'justify-end' : 'justify-start'}`}>
                        <div className={`max-w-[85%] p-4 rounded-2xl ${m.role === 'user' ? 'bg-bleu-de-france text-white rounded-tr-none' : 'bg-white text-gray-800 shadow-sm rounded-tl-none'}`}>
                          {m.text}
                        </div>
                      </div>
                    ))}
                  </div>
                  <form onSubmit={handleSubmit} className="p-4 bg-white border-t flex gap-2">
                    <input 
                      value={input} 
                      onChange={e => setInput(e.target.value)} 
                      placeholder="Zapytaj o zawodnika lub ligę..." 
                      className="flex-1 px-4 py-3 rounded-xl border focus:ring-2 focus:ring-bleu-de-france outline-none text-sm" 
                    />
                    <button className="bg-bleu-de-france text-white px-6 py-2 rounded-xl hover:bg-blue-800 transition uppercase font-bold text-xs">Wyślij</button>
                  </form>
                </div>
              </div>
            </section>
          );
        };

        const PlayerSection = () => (
          <section id="stars" className="py-24 bg-white">
            <div className="max-w-7xl mx-auto px-4">
              <div className="text-center mb-16">
                <h2 className="text-4xl md:text-5xl font-oswald font-bold mb-4 uppercase">Ikony i Nadzieje</h2>
                <div className="w-24 h-1 bg-rouge-france mx-auto"></div>
              </div>
              <div className="grid grid-cols-1 md:grid-cols-3 gap-12">
                {PLAYERS.map(p => (
                  <div key={p.id} className="group bg-gray-50 rounded-2xl overflow-hidden shadow-lg hover:shadow-2xl transition duration-300 border border-gray-100">
                    <div className="h-80 overflow-hidden relative">
                      <img src={p.image} className="w-full h-full object-cover group-hover:scale-105 transition duration-500" alt={p.name} />
                      <div className="absolute bottom-0 left-0 right-0 p-6 bg-gradient-to-t from-black text-white">
                        <p className="text-xs uppercase font-bold text-rouge-france mb-1">{p.position}</p>
                        <h3 className="text-2xl font-oswald font-bold">{p.name}</h3>
                      </div>
                    </div>
                    <div className="p-6">
                      <p className="text-sm text-bleu-de-france font-bold mb-3 uppercase tracking-wider">{p.team}</p>
                      <p className="text-gray-600 text-sm italic mb-6 leading-relaxed">"{p.description}"</p>
                      <div className="space-y-2">
                        {p.achievements.map((a, i) => (
                           <div key={i} className="flex items-center text-xs text-gray-700">
                              <span className="w-1.5 h-1.5 bg-rouge-france rounded-full mr-2"></span>
                              {a}
                           </div>
                        ))}
                      </div>
                    </div>
                  </div>
                ))}
              </div>
            </div>
          </section>
        );

        const App = () => (
          <div className="min-h-screen flex flex-col">
            <Navbar />
            <main>
              <Hero />
              <InfoCards />
              <PlayerSection />
              <StatsSection />
              <AIAnalyst />
            </main>
            <footer className="bg-black text-white py-16 text-center border-t-8 border-bleu-de-france">
              <p className="text-3xl font-oswald font-bold mb-4 uppercase tracking-tighter">FRENCH<span className="text-rouge-france">HOOPS</span></p>
              <div className="flex justify-center space-x-6 mb-8 text-gray-500 text-sm uppercase font-bold">
                <a href="#hero" className="hover:text-white">Home</a>
                <a href="#stars" className="hover:text-white">Players</a>
                <a href="#stats" className="hover:text-white">Stats</a>
              </div>
              <p className="text-gray-600 text-xs">© 2026 Portal Fanów Francuskiej Koszykówki. Created with Gemini AI Studio.</p>
            </footer>
          </div>
        );

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>
</html>
