<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PREMIUM TIPS | Elite Sports Analytics</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700;900&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; background-color: #020617; }
        .vip-gradient { background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%); }
        .card-blur { backdrop-filter: blur(10px); background: rgba(30, 41, 59, 0.7); }
    </style>
</head>
<body class="text-slate-100">

    <nav class="max-w-6xl mx-auto p-6 flex justify-between items-center">
        <div class="text-3xl font-black tracking-tighter italic">
            <span class="text-amber-500">PREMIUM</span>TIPS
        </div>
        <div class="flex items-center gap-4">
            <span id="userStatus" class="text-xs bg-slate-800 px-3 py-1 rounded-full text-slate-400">GUEST MODE</span>
            <button onclick="toggleVIP()" class="vip-gradient text-black font-bold px-5 py-2 rounded-lg text-sm hover:scale-105 transition">GET VIP ACCESS</button>
        </div>
    </nav>

    <header class="text-center py-20 px-4">
        <h1 class="text-5xl md:text-7xl font-black mb-4 tracking-tight">BEAT THE <span class="text-amber-500 italic">BOOKIES.</span></h1>
        <p class="text-slate-400 text-lg max-w-xl mx-auto">High-accuracy sports predictions powered by data. Join 5,000+ winning members today.</p>
    </header>

    <main class="max-w-4xl mx-auto p-4">
        <div class="flex bg-slate-900/50 p-1 rounded-xl mb-8 border border-slate-800">
            <button onclick="switchTab('free')" id="freeBtn" class="flex-1 py-3 rounded-lg font-bold transition bg-slate-800 text-white">FREE PICKS</button>
            <button onclick="switchTab('premium')" id="premiumBtn" class="flex-1 py-3 rounded-lg font-bold transition text-slate-400">VIP PREDICTIONS 🔥</button>
        </div>

        <div id="tipsFeed" class="space-y-4">
            </div>
    </main>

    <div id="vipModal" class="hidden fixed inset-0 bg-black/90 flex items-center justify-center p-6 z-50">
        <div class="bg-slate-900 border border-amber-500/50 p-8 rounded-3xl max-w-sm text-center">
            <div class="text-5xl mb-4">👑</div>
            <h2 class="text-2xl font-bold mb-2">Unlock VIP Tips</h2>
            <p class="text-slate-400 mb-6">Get 90%+ accuracy picks, daily parlays, and exclusive insights.</p>
            <button onclick="simulatePayment()" class="w-full vip-gradient text-black font-black py-4 rounded-xl mb-3">UPGRADE FOR $19/MO</button>
            <button onclick="closeModal()" class="text-slate-500 text-sm">Maybe later</button>
        </div>
    </div>

    <script>
        // --- DATA ---
        const tipsData = [
            { id: 1, type: 'free', match: 'Liverpool vs Everton', pick: 'Liverpool Win', odds: '1.45', time: '19:45' },
            { id: 2, type: 'free', match: 'Lakers vs Warriors', pick: 'Over 220.5', odds: '1.90', time: '02:00' },
            { id: 3, type: 'premium', match: 'Real Madrid vs Milan', pick: 'Madrid -1.5 AH', odds: '2.10', time: '21:00' },
            { id: 4, type: 'premium', match: 'Knicks vs Heat', pick: 'Knicks ML', odds: '1.85', time: '01:30' }
        ];

        let isVIP = false;
        let currentTab = 'free';

        // --- FUNCTIONS ---
        function render() {
            const feed = document.getElementById('tipsFeed');
            feed.innerHTML = '';

            const filtered = tipsData.filter(t => t.type === currentTab);

            filtered.forEach(tip => {
                const locked = tip.type === 'premium' && !isVIP;
                
                feed.innerHTML += `
                    <div class="card-blur border border-slate-800 p-6 rounded-2xl flex justify-between items-center transition hover:border-slate-600">
                        <div>
                            <div class="flex items-center gap-2 mb-1">
                                <span class="text-[10px] font-bold bg-slate-700 px-2 py-0.5 rounded text-slate-300 uppercase">${tip.time}</span>
                                ${tip.type === 'premium' ? '<span class="text-[10px] font-bold bg-amber-500 text-black px-2 py-0.5 rounded uppercase">VIP</span>' : ''}
                            </div>
                            <h3 class="text-xl font-bold">${tip.match}</h3>
                            <p class="text-lg ${locked ? 'blur-md select-none' : 'text-green-500 font-mono'}">
                                ${locked ? 'HIDDEN CONTENT' : tip.pick}
                            </p>
                        </div>
                        <div class="text-right">
                            <span class="text-xs text-slate-500 block uppercase tracking-widest">Odds</span>
                            <span class="text-2xl font-black">${locked ? '?.??' : tip.odds}</span>
                        </div>
                    </div>
                `;
            });
        }

        function switchTab(tab) {
            currentTab = tab;
            
            // UI Updates
            const freeBtn = document.getElementById('freeBtn');
            const premiumBtn = document.getElementById('premiumBtn');
            
            if(tab === 'free') {
                freeBtn.classList.add('bg-slate-800', 'text-white');
                premiumBtn.classList.remove('bg-slate-800', 'text-white');
                premiumBtn.classList.add('text-slate-400');
            } else {
                if(!isVIP) {
                    document.getElementById('vipModal').classList.remove('hidden');
                    return; // Don't switch tab if not VIP
                }
                premiumBtn.classList.add('bg-slate-800', 'text-white');
                freeBtn.classList.remove('bg-slate-800', 'text-white');
                freeBtn.classList.add('text-slate-400');
            }
            render();
        }

        function closeModal() {
            document.getElementById('vipModal').classList.add('hidden');
        }

        // Simulate a payment for demo purposes
        function simulatePayment() {
            alert("Redirecting to Payment Gateway...");
            setTimeout(() => {
                isVIP = true;
                document.getElementById('userStatus').innerText = "VIP MEMBER";
                document.getElementById('userStatus').classList.replace('bg-slate-800', 'bg-amber-900');
                document.getElementById('userStatus').classList.replace('text-slate-400', 'text-amber-200');
                closeModal();
                switchTab('premium');
            }, 1000);
        }

        // Initial Load
        render();
    </script>
</body>
</html>
