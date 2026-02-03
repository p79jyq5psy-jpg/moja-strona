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
        const { useState, useRef, useEffect, useMemo } = React;
        const { AreaChart, Area, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer } = Recharts;

        const PLAYERS = [
          {
            id: 'wemby',
            name: 'Victor Wembanyama',
            team: 'San Antonio Spurs',
            position: 'Center/Power Forward',
            image: 'https://images.unsplash.com/photo-1546519638-68e109498ffc?q=80&w=800&auto=format&fit=crop',
            description: 'Nazywany "Alienem", Wembanyama to największy talent w historii francuskiej koszykówki.',
            achievements: ['NBA Rookie of the Year 2024', 'Wicemistrz Olimpijski 2024', 'Lider bloków NBA']
          },
          {
            id: 'gobert',
            name: 'Rudy Gobert',
            team: 'Minnesota Timberwolves',
            position: 'Center',
            image: 'https://images.unsplash.com/photo-1519861531473-9200362f46b3?q=80&w=800&auto=format&fit=crop',
            description: '"The Stifle Tower" to filar defensywy reprezentacji Francji.',
            achievements: ['4x NBA Defensive Player of the Year', '3x NBA All-Star', 'Wicemistrz Olimpijski 2020, 2024']
          },
          {
            id: 'parker',
            name: 'Tony Parker',
            team: 'Legend (San Antonio Spurs)',
            position: 'Point Guard',
            image: 'https://images.unsplash.com/photo-1504450758481-7338eba7524a?q=80&w=800&auto=format&fit=crop',
            description: 'Najbardziej utytułowany francuski koszykarz w historii.',
            achievements: ['4x Mistrz NBA', 'NBA Finals MVP 2007', 'Mistrz Europy 2013']
          }
        ];

        const NBA_GROWTH_DATA = [
          { year: 1997, count: 1 }, { year: 2001, count: 2 }, { year: 2005, count: 5 },
          { year: 2010, count: 8 }, { year: 2015, count: 10 }, { year: 2020, count: 12 }, { year: 2024, count: 14 }
        ];

        const Navbar = () => (
          <nav className="sticky top-0 z-50 bg-white shadow-md border-b-4 border-bleu-de-france">
            <div className="max-w-7xl mx-auto px-4 flex justify-between h-20 items-center">
                <div className="flex items-center space-x-2">
                  <div className="w-10 h-10 bg-bleu-de-france flex items-center justify-center rounded-full text-white font-bold">FR</div>
                  <span className="text-2xl font-oswald font-bold">FRENCH<span className="text-rouge-france">HOOPS</span></span>
                </div>
                <div className="hidden md:flex space-x-8 font-semibold">
                  <a href="#hero" className="hover:text-bleu-de-france">Start</a>
                  <a href="#stars" className="hover:text-bleu-de-france">Gwiazdy</a>
                  <a href="#stats" className="hover:text-bleu-de-france">Rozwój</a>
                </div>
            </div>
          </nav>
        );

        const Hero = () => (
          <section id="hero" className="relative h-[60vh] flex items-center overflow-hidden bg-black text-white text-center">
            <div className="absolute inset-0 opacity-40">
              <img src="https://images.unsplash.com/photo-1544919982-b61976f0ba43?q=80&w=1920&auto=format&fit=crop" className="w-full h-full object-cover" />
            </div>
            <div className="relative z-10 w-full px-4">
                <h1 className="text-5xl md:text-7xl font-oswald font-bold mb-4">ZŁOTA ERA FRANCUSKIEGO BASKETU</h1>
                <p className="text-xl max-w-2xl mx-auto">Odkryj potęgę "Les Bleus" – od Parkera po Wembanyamę.</p>
            </div>
          </section>
        );

        const App = () => {
          return (
            <div className="min-h-screen flex flex-col">
              <Navbar />
              <Hero />
              <section id="stars" className="py-20 px-4 max-w-7xl mx-auto grid md:grid-cols-3 gap-8">
                {PLAYERS.map(p => (
                  <div key={p.id} className="bg-white rounded-xl shadow-lg overflow-hidden border">
                    <img src={p.image} className="h-64 w-full object-cover" />
                    <div className="p-6">
                      <h3 className="text-2xl font-oswald font-bold">{p.name}</h3>
                      <p className="text-bleu-de-france font-bold text-sm mb-2">{p.team}</p>
                      <p className="text-gray-600 text-sm mb-4">{p.description}</p>
                      <ul className="text-xs space-y-1">
                        {p.achievements.map((a, i) => <li key={i}>• {a}</li>)}
                      </ul>
                    </div>
                  </div>
                ))}
              </section>
              <footer className="bg-black text-white py-10 text-center">
                <p>© 2026 French Hoops Hub | Created with Gemini</p>
              </footer>
            </div>
          );
        }

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>
</html>
