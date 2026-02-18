# HowToThinkDeeper
How to think deeper
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Research Guide: The Workbench</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700&family=Inter:wght@300;400;600&display=swap');
        
        body {
            font-family: 'Inter', 'Noto Sans KR', sans-serif;
            background-color: #FDFBF7; /* Creamy White */
            color: #2D3748; /* Dark Charcoal */
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #F1F1F1;
        }
        ::-webkit-scrollbar-thumb {
            background: #CBD5E0;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #A0AEC0;
        }

        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            height: 300px;
            margin: 0 auto;
        }
        
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }

        .step-card {
            transition: all 0.3s ease;
        }
        .step-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }

        /* Active State for Navigation */
        .nav-item.active {
            background-color: #E2E8F0;
            border-left: 4px solid #D97706; /* Amber/Terracotta */
            font-weight: 600;
        }
    </style>
    
    <!-- Chosen Palette: Warm Neutral (Cream #FDFBF7) with Charcoal Text, Sage Green (#84A98C), and Terracotta/Amber (#D97706) Accents. -->
    <!-- Application Structure Plan: Dashboard layout. Left Sidebar for 7-step navigation. Main area displays content + interactive module per step. 
         Step 1: Text + Input Validator. 
         Step 2: Text + Pie Chart (80/20). 
         Step 3: Text + Bar Chart (Reading Funnel). 
         Step 4: Text + Note Comparison visual. 
         Step 5: Text + Line Chart (Diminishing Returns). 
         Step 6: Text + Interactive Schedule Grid. 
         Step 7: Text + Portfolio Accumulation Visual.
         Rationale: Step-by-step navigation encourages a linear learning journey while allowing non-linear reference. -->
    <!-- Visualization & Content Choices: 
         1. 80/20 Rule -> Pie Chart (Standard representation of proportions).
         2. Diminishing Returns -> Line Chart (Best for showing rate of change over time).
         3. Reading Funnel -> Bar Chart (Comparing quantities at different stages).
         4. Schedule -> HTML Grid (Interactive toggles for habit building).
         Libraries: Chart.js for graphs. Vanilla JS for logic. NO SVG/Mermaid. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

</head>
<body class="h-screen flex flex-col md:flex-row overflow-hidden">

    <!-- Mobile Header -->
    <header class="md:hidden bg-white border-b border-gray-200 p-4 flex justify-between items-center z-20">
        <h1 class="text-lg font-bold text-gray-800">📚 Smart Research</h1>
        <button id="mobile-menu-btn" class="text-gray-600 focus:outline-none text-2xl">
            &#9776; <!-- Hamburger Icon Unicode -->
        </button>
    </header>

    <!-- Sidebar Navigation -->
    <nav id="sidebar" class="bg-white border-r border-gray-200 w-full md:w-80 flex-shrink-0 h-full overflow-y-auto transform -translate-x-full md:translate-x-0 transition-transform duration-300 absolute md:relative z-10">
        <div class="p-6 border-b border-gray-100 hidden md:block">
            <h1 class="text-xl font-bold text-gray-800 tracking-tight">Smart Research<br><span class="text-sm font-normal text-gray-500">Workbench Guide</span></h1>
        </div>
        
        <div class="p-4 space-y-2" id="nav-container">
            <!-- Nav items injected by JS -->
        </div>

        <div class="p-6 mt-auto bg-gray-50 border-t border-gray-100">
            <div class="text-xs text-gray-500 mb-2">PROGRESS</div>
            <div class="w-full bg-gray-200 rounded-full h-2.5">
                <div id="progress-bar" class="bg-amber-600 h-2.5 rounded-full" style="width: 0%"></div>
            </div>
            <p class="text-xs text-right mt-1 text-gray-500"><span id="progress-text">0</span>% Completed</p>
        </div>
    </nav>

    <!-- Main Content Area -->
    <main class="flex-1 overflow-y-auto relative w-full h-full p-4 md:p-10 scroll-smooth">
        
        <!-- Intro / Welcome Screen (Default) -->
        <div id="welcome-screen" class="max-w-4xl mx-auto py-10">
            <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-8 md:p-12 text-center">
                <div class="text-6xl mb-6">🎓</div>
                <h2 class="text-3xl font-bold text-gray-800 mb-4">Smart Research Guide for Adults<br><span class="text-xl font-normal text-gray-600">성인을 위한 똑똑한 연구 습관 가이드</span></h2>
                <p class="text-gray-600 mb-8 max-w-2xl mx-auto leading-relaxed">
                    "Choose completion over perfection, essence over quantity."<br>
                    완벽함보다 완료를, 양보다 핵심을 선택하는 지적 성장 전략을 시작하세요.
                </p>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-left max-w-2xl mx-auto mb-10">
                    <div class="bg-amber-50 p-4 rounded-lg border border-amber-100">
                        <strong class="text-amber-800 block mb-1">English</strong>
                        Explore 7 key principles to transform how you learn and research efficiently.
                    </div>
                    <div class="bg-slate-50 p-4 rounded-lg border border-slate-100">
                        <strong class="text-slate-800 block mb-1">한국어</strong>
                        효율적으로 학습하고 연구하는 7가지 핵심 원칙을 탐험해보세요.
                    </div>
                </div>
                <button onclick="app.loadStep(0)" class="bg-gray-800 hover:bg-gray-900 text-white font-bold py-3 px-8 rounded-lg transition-colors shadow-lg transform hover:-translate-y-1">
                    Start Guide / 시작하기
                </button>
            </div>
        </div>

        <!-- Dynamic Content Container -->
        <div id="content-area" class="hidden max-w-5xl mx-auto pb-20">
            
            <!-- Header Section -->
            <div class="mb-8 border-b border-gray-200 pb-6">
                <div class="flex items-center space-x-3 text-sm font-medium text-amber-600 mb-2">
                    <span id="step-number" class="bg-amber-100 px-2 py-1 rounded">Step 01</span>
                    <span class="text-gray-400">|</span>
                    <span id="step-category">Category</span>
                </div>
                <h2 id="step-title-en" class="text-3xl md:text-4xl font-bold text-gray-900 mb-1">Title English</h2>
                <h3 id="step-title-kr" class="text-xl md:text-2xl text-gray-600 font-medium">Title Korean</h3>
            </div>

            <!-- Intro Box -->
            <div class="bg-white rounded-lg border border-gray-200 p-6 mb-8 shadow-sm">
                <p id="step-intro-en" class="text-gray-800 text-lg mb-2 leading-relaxed">English Intro</p>
                <p id="step-intro-kr" class="text-gray-500 text-base leading-relaxed">Korean Intro</p>
            </div>

            <!-- Split Layout: Principles & Interaction -->
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                
                <!-- Left: Principles List -->
                <div class="space-y-6">
                    <h4 class="text-lg font-bold text-gray-900 border-l-4 border-gray-800 pl-3">Core Principles / 핵심 원칙</h4>
                    <div id="principles-list" class="space-y-4">
                        <!-- Injected JS -->
                    </div>
                </div>

                <!-- Right: Interactive Module -->
                <div class="bg-gray-50 rounded-xl border border-gray-200 p-6 shadow-inner relative overflow-hidden">
                    <div class="absolute top-0 right-0 bg-gray-200 text-gray-600 text-xs font-bold px-3 py-1 rounded-bl-lg">INTERACTIVE / 실습</div>
                    
                    <h4 id="module-title" class="text-lg font-bold text-gray-800 mb-4">Activity</h4>
                    
                    <!-- Content injected here -->
                    <div id="interaction-container" class="w-full"></div>
                    
                    <div id="module-feedback" class="mt-4 p-3 bg-white rounded border border-gray-200 text-sm hidden"></div>
                </div>

            </div>

            <!-- Footer Navigation -->
            <div class="mt-12 flex justify-between items-center border-t border-gray-200 pt-8">
                <button id="prev-btn" class="text-gray-500 hover:text-gray-800 font-medium px-4 py-2 rounded transition-colors disabled:opacity-30">
                    &larr; Previous
                </button>
                <button id="next-btn" class="bg-gray-800 hover:bg-gray-900 text-white font-bold py-3 px-8 rounded shadow-md transition-all">
                    Next Step &rarr;
                </button>
            </div>

        </div>

    </main>

    <!-- JavaScript Application Logic -->
    <script>
        // Data Store
        const guideData = [
            {
                id: 1,
                category: "Questioning (질문)",
                titleEn: "Choosing Worthwhile Questions",
                titleKr: "가치 있는 질문 선정",
                introEn: "Research energy comes from genuine curiosity. Before diving in, validate your question.",
                introKr: "연구의 에너지는 '진짜 궁금함'에서 나옵니다. 시작하기 전, 질문을 점검하세요.",
                principles: [
                    { t: "Follow Genuine Curiosity", d: "Choose topics that genuinely interest you, not out of obligation.", k: "의무감이 아닌, 당신을 움직이게 하는 흥미로운 주제를 택하세요." },
                    { t: "Be Specific", d: "Narrow down vague goals like 'Climate Change' to specific questions.", k: "'기후 변화' 같이 막연한 목표 대신 구체적인 질문으로 좁히세요." },
                    { t: "The 'So What?' Test", d: "Ask yourself what insight this research will provide.", k: "이 연구가 어떤 통찰을 줄지 자문하고 가치가 있을 때 시작하세요." },
                    { t: "Idea Backlog", d: "Save interesting topics for later to focus on the present.", k: "당장 할 수 없는 주제는 저장해두고 현재에 집중하세요." }
                ],
                interactionType: "validator"
            },
            {
                id: 2,
                category: "Scoping (범위)",
                titleEn: "Scoping & Constraints",
                titleKr: "현실적인 범위와 관리",
                introEn: "Results come from realistic constraints. Apply the 80/20 rule to maximize efficiency.",
                introKr: "제약이 있을 때 비로소 결과물이 나옵니다. 80/20 법칙을 적용해 효율을 극대화하세요.",
                principles: [
                    { t: "Define Deliverables", d: "Set a specific goal like a '5-page summary' before starting.", k: "시작 전 '5페이지 요약본' 같은 구체적 산출물을 정하세요." },
                    { t: "The 80/20 Rule", d: "80% of insights come from 20% of sources.", k: "핵심 통찰의 80%는 상위 20% 자료에서 나옵니다." },
                    { t: "Time-boxing", d: "Set strict deadlines (e.g., '2 weeks').", k: "'딱 2주'와 같이 마감 기한을 엄격히 설정하세요." },
                    { t: "Micro-tasks", d: "Break tasks into 10-30 minute chunks.", k: "작업을 10-30분 단위로 쪼개 자투리 시간을 활용하세요." }
                ],
                interactionType: "chart-8020"
            },
            {
                id: 3,
                category: "Reading (자료)",
                titleEn: "Reading & Evaluating",
                titleKr: "효율적인 독서와 평가",
                introEn: "Abandon perfectionism. Use a funnel approach to filter information effectively.",
                introKr: "완벽주의를 버리세요. 깔때기 방식을 사용해 정보를 효율적으로 걸러내세요.",
                principles: [
                    { t: "Scan Wide, Drill Deep", d: "Skim 20 articles, read 3 in depth.", k: "20개를 훑어보고 3개만 정독하세요." },
                    { t: "Triangulation", d: "Accept facts if 3 independent sources agree.", k: "3개의 독립된 출처가 일치하면 사실로 수용하세요." },
                    { t: "Long-half-life Knowledge", d: "Prioritize books over fleeting news.", k: "휘발성 뉴스보다 시간이 지나도 가치 있는 책을 우선하세요." },
                    { t: "Hierarchical Reading", d: "TOC → Summary → Relevant Sections → Deep Reading.", k: "목차 → 요약 → 발췌 → 정독 순으로 에너지를 배분하세요." }
                ],
                interactionType: "chart-funnel"
            },
            {
                id: 4,
                category: "Note-Taking (기록)",
                titleEn: "Smart Note-Taking",
                titleKr: "똑똑한 노트 필기",
                introEn: "Writing is an investment. Transform information into your own knowledge assets.",
                introKr: "기록은 투자입니다. 정보를 나만의 지식 자산으로 변환하세요.",
                principles: [
                    { t: "Use Your Own Language", d: "Don't copy; rephrase in your own words.", k: "단순히 베끼지 말고 자신의 언어로 재해석하세요." },
                    { t: "Context & Source", d: "Record 'why important' and 'where from'.", k: "'왜 중요한지'와 '출처'를 함께 적으세요." },
                    { t: "Atomic Notes", d: "One idea per note for easy reassembly.", k: "하나의 노트에는 하나의 아이디어만 담으세요." },
                    { t: "Build a Network", d: "Link notes to create connections.", k: "태그와 링크로 지식 간의 연결 고리를 만드세요." }
                ],
                interactionType: "note-tool"
            },
            {
                id: 5,
                category: "Synthesis (융합)",
                titleEn: "Synthesizing & Stopping",
                titleKr: "융합 및 종료 시점",
                introEn: "Know when to stop. Understand the law of diminishing returns in research.",
                introKr: "멈출 때를 아세요. 연구에서 수확 체감의 법칙을 이해해야 합니다.",
                principles: [
                    { t: "Law of Diminishing Returns", d: "Stop if sources repeat obvious info.", k: "뻔한 내용이 반복되면 조사를 멈추세요." },
                    { t: "Avoid Sunk Cost Fallacy", d: "Change direction if stuck, regardless of time spent.", k: "시간이 아까워도 답이 안 보이면 과감히 방향을 트세요." },
                    { t: "Public Synthesis", d: "Explain to others to solidify knowledge.", k: "남에게 설명하며 지식을 내 것으로 만드세요." },
                    { t: "Cross-pollination", d: "Apply concepts to different fields.", k: "다른 분야의 개념을 적용해 통찰을 얻으세요." }
                ],
                interactionType: "chart-curve"
            },
            {
                id: 6,
                category: "Momentum (동기)",
                titleEn: "Maintaining Momentum",
                titleKr: "추진력 유지",
                introEn: "Create a sustainable system for research without external deadlines.",
                introKr: "마감이 없는 연구를 지속할 수 있는 시스템을 만드세요.",
                principles: [
                    { t: "Establish a Routine", d: "Formalize 'research time' weekly.", k: "매주 '연구 시간'을 공식화하세요." },
                    { t: "Ride the Energy Wave", d: "Dive deep when inspiration strikes.", k: "몰입이 잘 될 때 깊게 파고드세요." },
                    { t: "Accountability Mechanism", d: "Declare deadlines to friends.", k: "지인에게 마감을 선언하세요." },
                    { t: "Interleaving Difficulty", d: "Switch between hard and easy tasks.", k: "어렵고 쉬운 작업을 번갈아 하세요." }
                ],
                interactionType: "schedule-grid"
            },
            {
                id: 7,
                category: "Mindset (마인드)",
                titleEn: "Long-term Mindset",
                titleKr: "장기적 마인드셋",
                introEn: "View your knowledge as a growing portfolio. Reward your progress.",
                introKr: "지식을 성장하는 포트폴리오로 바라보세요. 과정을 보상하세요.",
                principles: [
                    { t: "Knowledge Portfolio", d: "Treat projects as assets; accumulate principles.", k: "프로젝트를 자산으로 여기고 원칙을 축적하세요." },
                    { t: "Reward the Process", d: "Give yourself clear rewards at milestones.", k: "마일스톤 달성 시 확실히 보상하세요." }
                ],
                interactionType: "portfolio-vis"
            }
        ];

        // App Logic
        const app = {
            currentStepIndex: 0,
            chartInstance: null,

            init: () => {
                app.renderNav();
                app.setupMobileMenu();
                // Check if hash exists to load specific step
                // Default is welcome screen
            },

            setupMobileMenu: () => {
                const btn = document.getElementById('mobile-menu-btn');
                const sidebar = document.getElementById('sidebar');
                btn.addEventListener('click', () => {
                    sidebar.classList.toggle('-translate-x-full');
                });
            },

            renderNav: () => {
                const container = document.getElementById('nav-container');
                container.innerHTML = guideData.map((step, index) => `
                    <button onclick="app.loadStep(${index})" class="nav-item w-full text-left px-4 py-3 rounded-lg text-sm transition-colors hover:bg-gray-100 flex items-center justify-between group ${app.currentStepIndex === index ? 'active' : ''}" id="nav-${index}">
                        <div>
                            <span class="block font-semibold text-gray-700 group-hover:text-gray-900">0${index + 1}. ${step.category.split(' ')[0]}</span>
                            <span class="block text-xs text-gray-500">${step.titleKr}</span>
                        </div>
                    </button>
                `).join('');
            },

            updateProgress: () => {
                const pct = Math.round(((app.currentStepIndex + 1) / guideData.length) * 100);
                document.getElementById('progress-bar').style.width = `${pct}%`;
                document.getElementById('progress-text').innerText = pct;
                
                // Update nav styling
                document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));
                const activeNav = document.getElementById(`nav-${app.currentStepIndex}`);
                if (activeNav) activeNav.classList.add('active');
            },

            loadStep: (index) => {
                app.currentStepIndex = index;
                const step = guideData[index];

                // Hide Welcome, Show Content
                document.getElementById('welcome-screen').classList.add('hidden');
                document.getElementById('content-area').classList.remove('hidden');

                // Close mobile menu if open
                if(window.innerWidth < 768) {
                    document.getElementById('sidebar').classList.add('-translate-x-full');
                }

                // Update Header Content
                document.getElementById('step-number').innerText = `Step 0${step.id}`;
                document.getElementById('step-category').innerText = step.category;
                document.getElementById('step-title-en').innerText = step.titleEn;
                document.getElementById('step-title-kr').innerText = step.titleKr;
                document.getElementById('step-intro-en').innerText = step.introEn;
                document.getElementById('step-intro-kr').innerText = step.introKr;

                // Render Principles
                const principlesContainer = document.getElementById('principles-list');
                principlesContainer.innerHTML = step.principles.map(p => `
                    <div class="bg-white p-4 rounded-lg border border-gray-100 shadow-sm step-card hover:border-amber-200">
                        <h5 class="font-bold text-gray-800 text-lg mb-1">${p.t}</h5>
                        <p class="text-sm text-gray-600 mb-2">${p.d}</p>
                        <p class="text-sm text-gray-500 font-medium bg-gray-50 p-2 rounded border-l-2 border-gray-300">🇰🇷 ${p.k}</p>
                    </div>
                `).join('');

                // Update Buttons
                const prevBtn = document.getElementById('prev-btn');
                const nextBtn = document.getElementById('next-btn');
                
                prevBtn.disabled = index === 0;
                prevBtn.onclick = () => app.loadStep(index - 1);
                
                if (index === guideData.length - 1) {
                    nextBtn.innerHTML = "Finish Journey 🎉";
                    nextBtn.onclick = () => alert("Congratulations! You've completed the guide. Now go research!");
                } else {
                    nextBtn.innerHTML = "Next Step &rarr;";
                    nextBtn.onclick = () => app.loadStep(index + 1);
                }

                app.updateProgress();
                app.renderInteraction(step);
            },

            renderInteraction: (step) => {
                const container = document.getElementById('interaction-container');
                const title = document.getElementById('module-title');
                container.innerHTML = ''; // Clear previous
                document.getElementById('module-feedback').classList.add('hidden');
                
                // Destroy previous chart if exists
                if (app.chartInstance) {
                    app.chartInstance.destroy();
                    app.chartInstance = null;
                }

                if (step.interactionType === 'validator') {
                    title.innerText = "Question Validator (질문 진단기)";
                    container.innerHTML = `
                        <div class="space-y-4">
                            <label class="block text-sm font-medium text-gray-700">Type your research topic/question:</label>
                            <input type="text" id="q-input" class="w-full p-3 border border-gray-300 rounded focus:ring-2 focus:ring-amber-500 focus:outline-none" placeholder="e.g., Climate Change">
                            <button onclick="app.validateQuestion()" class="w-full bg-amber-600 text-white font-bold py-2 rounded hover:bg-amber-700">Check Quality</button>
                        </div>
                    `;
                } else if (step.interactionType === 'chart-8020') {
                    title.innerText = "The 80/20 Efficiency Visualizer";
                    container.innerHTML = `
                        <p class="text-sm text-gray-600 mb-4">See how focused effort yields majority results.</p>
                        <div class="chart-container">
                            <canvas id="chart-canvas"></canvas>
                        </div>
                    `;
                    app.renderChart8020();
                } else if (step.interactionType === 'chart-funnel') {
                    title.innerText = "Reading Funnel (독서 깔때기)";
                    container.innerHTML = `
                        <p class="text-sm text-gray-600 mb-4">Drastically reduce quantity to increase quality.</p>
                        <div class="chart-container">
                            <canvas id="chart-canvas"></canvas>
                        </div>
                    `;
                    app.renderChartFunnel();
                } else if (step.interactionType === 'note-tool') {
                    title.innerText = "Note Rephraser (재해석 연습)";
                    container.innerHTML = `
                        <div class="space-y-3">
                            <div class="p-3 bg-red-50 border border-red-100 rounded text-xs text-red-800">
                                <strong>Original Text:</strong> "Photosynthesis is the process used by plants to convert light energy into chemical energy."
                            </div>
                            <textarea id="note-input" rows="3" class="w-full p-2 border border-gray-300 rounded text-sm" placeholder="Write in your own words (Why is this important for your topic?)..."></textarea>
                            <button onclick="app.checkNote()" class="w-full bg-slate-600 text-white font-bold py-2 rounded hover:bg-slate-700">Save Atomic Note</button>
                        </div>
                    `;
                } else if (step.interactionType === 'chart-curve') {
                    title.innerText = "Diminishing Returns (수확 체감)";
                    container.innerHTML = `
                        <p class="text-sm text-gray-600 mb-2">Drag slider to add research hours.</p>
                        <input type="range" min="1" max="10" value="3" class="w-full mb-4 accent-amber-600" oninput="app.updateCurve(this.value)">
                        <div class="chart-container">
                            <canvas id="chart-canvas"></canvas>
                        </div>
                    `;
                    app.renderChartCurve(3);
                } else if (step.interactionType === 'schedule-grid') {
                    title.innerText = "Weekly Routine Builder";
                    container.innerHTML = `
                        <p class="text-sm text-gray-600 mb-3">Click cells to set "Deep Research" blocks.</p>
                        <div class="grid grid-cols-7 gap-1 mb-2 text-center text-xs font-bold text-gray-500">
                            <div>Mon</div><div>Tue</div><div>Wed</div><div>Thu</div><div>Fri</div><div>Sat</div><div>Sun</div>
                        </div>
                        <div class="grid grid-cols-7 gap-2" id="habit-grid">
                            ${Array(14).fill(0).map((_, i) => `<div onclick="this.classList.toggle('bg-amber-500'); this.classList.toggle('text-white');" class="h-10 bg-white border border-gray-200 rounded cursor-pointer hover:bg-amber-100 flex items-center justify-center text-xs text-gray-400 transition-colors">${i < 7 ? 'AM' : 'PM'}</div>`).join('')}
                        </div>
                        <div class="mt-3 text-xs text-center text-gray-500">Consistency > Intensity</div>
                    `;
                } else if (step.interactionType === 'portfolio-vis') {
                    title.innerText = "Knowledge Portfolio";
                    container.innerHTML = `
                        <div class="flex flex-col items-center justify-center space-y-4 h-64 bg-white rounded border border-gray-100">
                            <div class="flex items-end space-x-2 h-32" id="portfolio-stack">
                                <div class="w-8 bg-gray-300 h-10 rounded-t" title="Project A"></div>
                                <div class="w-8 bg-gray-400 h-16 rounded-t" title="Project B"></div>
                                <div class="w-8 bg-amber-500 h-24 rounded-t animate-bounce" title="Current Project"></div>
                            </div>
                            <p class="text-sm text-gray-600 text-center px-4">Each project builds your foundation.<br>Keep going!</p>
                            <button onclick="confetti()" class="px-4 py-2 bg-green-600 text-white rounded shadow text-sm">Collect Reward 🎁</button>
                        </div>
                    `;
                }
            },

            // --- Interaction Functions ---

            validateQuestion: () => {
                const input = document.getElementById('q-input').value;
                const feedback = document.getElementById('module-feedback');
                feedback.classList.remove('hidden');
                
                if (input.length < 10) {
                    feedback.innerHTML = `<span class="text-red-600 font-bold">Too Short.</span> Try adding more context.`;
                    feedback.className = "mt-4 p-3 bg-red-50 rounded border border-red-200 text-sm";
                } else if (input.split(' ').length < 4) {
                    feedback.innerHTML = `<span class="text-amber-600 font-bold">Too Vague.</span> Use the format: "How does [X] affect [Y]?"`;
                    feedback.className = "mt-4 p-3 bg-amber-50 rounded border border-amber-200 text-sm";
                } else {
                    feedback.innerHTML = `<span class="text-green-600 font-bold">Good Specificity!</span> Now ask: "So What?"`;
                    feedback.className = "mt-4 p-3 bg-green-50 rounded border border-green-200 text-sm";
                }
            },

            checkNote: () => {
                const input = document.getElementById('note-input').value;
                const feedback = document.getElementById('module-feedback');
                feedback.classList.remove('hidden');
                
                if (input.toLowerCase().includes("photosynthesis") && input.length > 20) {
                     feedback.innerHTML = `<span class="text-green-600 font-bold">Great!</span> You captured the concept in your own words.`;
                     feedback.className = "mt-4 p-3 bg-green-50 rounded border border-green-200 text-sm";
                } else {
                    feedback.innerHTML = `<span class="text-gray-600">Tip:</span> Try to explain *why* this matters to your research, not just what it is.`;
                    feedback.className = "mt-4 p-3 bg-gray-50 rounded border border-gray-200 text-sm";
                }
            },

            // --- Chart Renderers ---

            renderChart8020: () => {
                const ctx = document.getElementById('chart-canvas').getContext('2d');
                app.chartInstance = new Chart(ctx, {
                    type: 'doughnut',
                    data: {
                        labels: ['Key Insights (핵심)', 'Noise/Filler (나머지)'],
                        datasets: [{
                            data: [80, 20],
                            backgroundColor: ['#D97706', '#E2E8F0'], // Amber, Slate
                            borderWidth: 0
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: { position: 'bottom' },
                            tooltip: { callbacks: { label: (ctx) => ` ${ctx.raw}% Value from 20% Sources` } }
                        }
                    }
                });
            },

            renderChartFunnel: () => {
                const ctx = document.getElementById('chart-canvas').getContext('2d');
                app.chartInstance = new Chart(ctx, {
                    type: 'bar',
                    data: {
                        labels: ['Skim (훑기)', 'Select (선별)', 'Deep Read (정독)'],
                        datasets: [{
                            label: 'Number of Sources',
                            data: [20, 5, 3],
                            backgroundColor: ['#CBD5E0', '#A0AEC0', '#D97706']
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        indexAxis: 'y',
                        plugins: {
                            legend: { display: false }
                        },
                        scales: {
                            x: { beginAtZero: true }
                        }
                    }
                });
            },

            renderChartCurve: (initialValue) => {
                const ctx = document.getElementById('chart-canvas').getContext('2d');
                const generateData = () => {
                    const data = [];
                    for(let i=0; i<=10; i++) {
                        // Logarithmic curve: y = ln(x + 1) * scale
                        data.push(Math.log(i + 1) * 30);
                    }
                    return data;
                };

                app.chartInstance = new Chart(ctx, {
                    type: 'line',
                    data: {
                        labels: Array.from({length: 11}, (_, i) => i + 'h'),
                        datasets: [{
                            label: 'Insight Gained',
                            data: generateData(),
                            borderColor: '#4A5568',
                            backgroundColor: 'rgba(74, 85, 104, 0.1)',
                            fill: true,
                            tension: 0.4,
                            pointRadius: (ctx) => ctx.dataIndex == initialValue ? 6 : 0,
                            pointBackgroundColor: '#D97706'
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        scales: {
                            y: { display: false, title: {display: true, text: 'Value'} },
                            x: { title: {display: true, text: 'Time Spent'} }
                        },
                        plugins: {
                            annotation: {
                                annotations: {
                                    line1: {
                                        type: 'line',
                                        xMin: initialValue,
                                        xMax: initialValue,
                                        borderColor: '#D97706',
                                        borderWidth: 2,
                                        label: { content: 'Stop Here?', enabled: true, position: 'start' }
                                    }
                                }
                            }
                        }
                    }
                });
            },

            updateCurve: (val) => {
                if(app.chartInstance) {
                    app.chartInstance.data.datasets[0].pointRadius = (ctx) => ctx.dataIndex == val ? 8 : 0;
                    app.chartInstance.update();
                    
                    const feedback = document.getElementById('module-feedback');
                    feedback.classList.remove('hidden');
                    if (val > 6) {
                        feedback.innerHTML = `<span class="text-red-600 font-bold">Diminishing Returns!</span> You are spending lots of time for very little extra insight. Stop and write.`;
                    } else if (val < 2) {
                        feedback.innerHTML = `Too shallow. Dig deeper.`;
                    } else {
                        feedback.innerHTML = `<span class="text-green-600 font-bold">Optimal Zone.</span> High insight, reasonable time.`;
                    }
                }
            }
        };

        // Simple visual reward function
        function confetti() {
            const btn = document.querySelector('button[onclick="confetti()"]');
            const originalText = btn.innerText;
            btn.innerText = "🎉 Yay! 🎉";
            btn.classList.add('bg-amber-500');
            setTimeout(() => {
                btn.innerText = originalText;
                btn.classList.remove('bg-amber-500');
            }, 2000);
        }

        // Initialize
        document.addEventListener('DOMContentLoaded', app.init);

    </script>
</body>
</html>
