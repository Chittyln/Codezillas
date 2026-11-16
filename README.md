# Codezillas
<!DOCTYPE html>
<html lang="en" class="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>CODEZILLA – Multi-Language Programming Quiz Game</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=JetBrains+Mono:wght@400;500;600;700&display=swap" rel="stylesheet" />
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: {
            sans: ['Inter', 'sans-serif'],
            mono: ['JetBrains Mono', 'monospace'],
          },
          colors: {
            navy: {
              950: '#070B19',
              900: '#0B1126',
              800: '#111936',
              700: '#18234A',
            },
            electric: {
              purple: '#8B5CF6',
              blue: '#3B82F6',
              cyan: '#06B6D4',
            }
          }
        }
      }
    }
  </script>
  <style>
    * {
      scrollbar-width: thin;
      scrollbar-color: #312E81 #0B1126;
    }
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: #0B1126;
    }
    ::-webkit-scrollbar-thumb {
      background: #312E81;
      border-radius: 9999px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #4F46E5;
    }
    body {
      background-color: #070B19;
      background-image:
        radial-gradient(circle at 15% 15%, rgba(139, 92, 246, 0.14) 0%, transparent 42%),
        radial-gradient(circle at 85% 20%, rgba(59, 130, 246, 0.14) 0%, transparent 45%),
        radial-gradient(circle at 50% 90%, rgba(6, 182, 212, 0.08) 0%, transparent 50%);
      color: #F8FAFC;
      min-height: 100vh;
    }
    .glass-card {
      background: linear-gradient(145deg, rgba(17, 25, 54, 0.85), rgba(11, 17, 38, 0.92));
      backdrop-filter: blur(14px);
      -webkit-backdrop-filter: blur(14px);
      border: 1px solid rgba(139, 92, 246, 0.22);
      box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.6);
    }
    .glass-card-hover {
      transition: all 0.28s cubic-bezier(0.4, 0, 0.2, 1);
    }
    .glass-card-hover:hover {
      transform: translateY(-4px);
      border-color: rgba(139, 92, 246, 0.55);
      box-shadow: 0 18px 36px -12px rgba(99, 102, 241, 0.28);
    }
    .gradient-btn {
      background: linear-gradient(135deg, #7C3AED 0%, #3B82F6 100%);
      transition: all 0.25s ease;
    }
    .gradient-btn:hover {
      background: linear-gradient(135deg, #8B5CF6 0%, #2563EB 100%);
      box-shadow: 0 8px 24px -4px rgba(124, 58, 237, 0.5);
      transform: translateY(-1px);
    }
    .nav-item-active {
      background: linear-gradient(90deg, rgba(139, 92, 246, 0.24) 0%, rgba(59, 130, 246, 0.12) 100%);
      border-left: 3px solid #8B5CF6;
      color: #FFFFFF;
    }
    .fade-in {
      animation: fadeIn 0.35s ease-out forwards;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(8px); }
      to { opacity: 1; transform: translateY(0); }
    }
    .pulse-glow {
      animation: pulseGlow 2.8s infinite;
    }
    @keyframes pulseGlow {
      0%, 100% { box-shadow: 0 0 16px rgba(139, 92, 246, 0.3); }
      50% { box-shadow: 0 0 28px rgba(59, 130, 246, 0.55); }
    }
  </style>
</head>
<body class="antialiased selection:bg-purple-500 selection:text-white">

  <!-- Mobile Sidebar Backdrop -->
  <div id="sidebarBackdrop" onclick="toggleSidebar(false)" class="fixed inset-0 bg-black/70 z-30 hidden lg:hidden backdrop-blur-sm transition-opacity"></div>

  <div class="flex min-h-screen">
    <!-- Sidebar Navigation -->
    <aside id="sidebar" class="fixed lg:sticky top-0 left-0 z-40 h-screen w-72 bg-navy-900/95 border-r border-indigo-500/20 flex flex-col justify-between transition-transform duration-300 -translate-x-full lg:translate-x-0 backdrop-blur-xl">
      <div>
        <!-- Brand Logo -->
        <div class="px-6 py-6 flex items-center justify-between border-b border-indigo-500/15">
          <div class="flex items-center gap-3 cursor-pointer" onclick="navigateTo('dashboard')">
            <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-purple-600 via-indigo-600 to-blue-500 flex items-center justify-center shadow-lg shadow-purple-600/30 pulse-glow">
              <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" stroke-width="2.2" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z" />
              </svg>
            </div>
            <div>
              <span class="text-xl font-extrabold tracking-wider bg-gradient-to-r from-white via-purple-200 to-blue-300 bg-clip-text text-transparent">CODEZILLA</span>
              <p class="text-[11px] text-indigo-300/75 font-medium tracking-wide uppercase">Code &amp; Conquer</p>
            </div>
          </div>
          <button onclick="toggleSidebar(false)" class="lg:hidden text-slate-400 hover:text-white p-1.5 rounded-lg hover:bg-white/5">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg>
          </button>
        </div>

        <!-- Navigation Menu -->
        <nav class="px-4 py-6 space-y-1.5">
          <p class="px-3 text-[11px] font-semibold uppercase tracking-wider text-slate-400/80 mb-2">Main Menu</p>
          <button id="nav-dashboard" onclick="navigateTo('dashboard')" class="nav-btn nav-item-active w-full flex items-center gap-3.5 px-4 py-3 rounded-xl text-sm font-medium text-slate-300 hover:text-white hover:bg-white/5 transition-all">
            <svg class="w-5 h-5 text-purple-400" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z"/>
            </svg>
            <span>Dashboard</span>
          </button>

          <button id="nav-languages" onclick="navigateTo('languages')" class="nav-btn w-full flex items-center gap-3.5 px-4 py-3 rounded-xl text-sm font-medium text-slate-300 hover:text-white hover:bg-white/5 transition-all">
            <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"/>
            </svg>
            <span>Languages &amp; Levels</span>
            <span class="ml-auto text-[11px] font-semibold px-2 py-0.5 rounded-full bg-blue-500/20 text-blue-300 border border-blue-500/30">6</span>
          </button>

          <button id="nav-quiz" onclick="navigateTo('quiz')" class="nav-btn w-full flex items-center gap-3.5 px-4 py-3 rounded-xl text-sm font-medium text-slate-300 hover:text-white hover:bg-white/5 transition-all">
            <svg class="w-5 h-5 text-cyan-400" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"/>
            </svg>
            <span>Quiz Arena</span>
            <span class="ml-auto w-2 h-2 rounded-full bg-emerald-400 animate-ping"></span>
          </button>

          <button id="nav-performance" onclick="navigateTo('performance')" class="nav-btn w-full flex items-center gap-3.5 px-4 py-3 rounded-xl text-sm font-medium text-slate-300 hover:text-white hover:bg-white/5 transition-all">
            <svg class="w-5 h-5 text-indigo-400" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"/>
            </svg>
            <span>Performance Analytics</span>
          </button>
        </nav>

        <!-- Quick Language Jump -->
        <div class="px-4 mt-2">
          <p class="px-3 text-[11px] font-semibold uppercase tracking-wider text-slate-400/80 mb-2">Quick Launch Track</p>
          <div id="sidebarQuickLangs" class="space-y-1"></div>
        </div>
      </div>

      <!-- Student Profile / XP Card -->
      <div class="p-4 border-t border-indigo-500/15">
        <div class="p-3.5 rounded-2xl bg-gradient-to-br from-indigo-950/90 to-purple-950/70 border border-purple-500/25">
          <div class="flex items-center gap-3">
            <div class="w-10 h-10 rounded-full bg-gradient-to-tr from-purple-500 to-blue-500 flex items-center justify-center font-bold text-sm text-white shadow-md">
              AR
            </div>
            <div class="min-w-0 flex-1">
              <p class="text-sm font-semibold text-white truncate">Aarav Sharma</p>
              <p class="text-xs text-purple-300 truncate">B.Tech CS • Sem 5</p>
            </div>
            <span class="px-2 py-0.5 text-[11px] font-bold rounded-md bg-purple-500/25 text-purple-200 border border-purple-400/30">Lvl 12</span>
          </div>
          <div class="mt-3">
            <div class="flex justify-between text-[11px] text-slate-300 mb-1">
              <span>Season XP</span>
              <span id="sidebarXpText" class="font-mono text-purple-300">2,450 / 3,000</span>
            </div>
            <div class="w-full h-1.5 bg-navy-950 rounded-full overflow-hidden">
              <div id="sidebarXpBar" class="h-full bg-gradient-to-r from-purple-500 to-blue-400 rounded-full transition-all duration-500" style="width: 81.6%"></div>
            </div>
          </div>
        </div>
      </div>
    </aside>

    <!-- Main Content Area -->
    <div class="flex-1 flex flex-col min-w-0">
      <!-- Top Header -->
      <header class="sticky top-0 z-20 bg-navy-950/80 backdrop-blur-xl border-b border-indigo-500/15 px-4 sm:px-8 py-4">
        <div class="max-w-7xl mx-auto flex items-center justify-between gap-4">
          <div class="flex items-center gap-3">
            <button onclick="toggleSidebar(true)" class="lg:hidden p-2 rounded-xl bg-navy-800 border border-indigo-500/25 text-slate-200 hover:text-white">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"/></svg>
            </button>
            <div>
              <h1 id="pageTitle" class="text-lg sm:text-xl font-bold text-white tracking-tight">Student Dashboard</h1>
              <p id="pageSubtitle" class="text-xs text-slate-400 hidden sm:block">Track your multi-language mastery, quiz streaks, and coding accuracy</p>
            </div>
          </div>

          <div class="flex items-center gap-3">
            <!-- Active Study Streak -->
            <div class="hidden sm:flex items-center gap-2 px-3.5 py-1.5 rounded-xl bg-amber-500/10 border border-amber-500/25 text-amber-300 text-xs font-semibold">
              <span>🔥</span>
              <span>7-Day Streak</span>
            </div>

            <!-- Live Session Timer -->
            <div class="flex items-center gap-2 px-3.5 py-1.5 rounded-xl bg-navy-800/90 border border-indigo-500/25 text-xs font-mono text-indigo-200">
              <span class="w-2 h-2 rounded-full bg-emerald-400"></span>
              <span id="liveSessionClock">00:00</span>
            </div>

            <button onclick="navigateTo('languages')" class="gradient-btn px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold text-white flex items-center gap-2 shadow-lg">
              <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2.2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z"/><path stroke-linecap="round" stroke-linejoin="round" d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
              <span>Start Quiz</span>
            </button>
          </div>
        </div>
      </header>

      <!-- Main View Container -->
      <main class="flex-1 px-4 sm:px-8 py-6 max-w-7xl w-full mx-auto">

        <!-- ==================== VIEW 1: DASHBOARD ==================== -->
        <section id="view-dashboard" class="space-y-6 fade-in">
          <!-- Welcome Banner -->
          <div class="relative overflow-hidden rounded-3xl p-6 sm:p-8 bg-gradient-to-r from-indigo-900/90 via-purple-900/80 to-blue-900/80 border border-purple-400/25 shadow-2xl">
            <div class="absolute -right-12 -top-12 w-64 h-64 bg-purple-500/20 rounded-full blur-3xl pointer-events-none"></div>
            <div class="absolute right-24 -bottom-16 w-56 h-56 bg-blue-500/20 rounded-full blur-3xl pointer-events-none"></div>

            <div class="relative z-10 flex flex-col lg:flex-row lg:items-center justify-between gap-6">
              <div class="space-y-2 max-w-2xl">
                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-white/10 border border-white/15 text-xs font-medium text-purple-200">
                  <span>⚡ Academic Semester Challenge • Fall 2026</span>
                </div>
                <h2 class="text-2xl sm:text-3xl font-extrabold text-white tracking-tight">
                  Welcome back, Aarav! Ready to level up your code?
                </h2>
                <p class="text-sm sm:text-base text-indigo-100/85 leading-relaxed">
                  You've improved your problem-solving accuracy by <span class="font-bold text-emerald-300" id="bannerImprovement">+28.5%</span> this month. Complete <span class="font-semibold text-white">Python Level 2</span> or <span class="font-semibold text-white">CSS Level 1</span> next to unlock new badges!
                </p>
              </div>
              <div class="flex flex-wrap sm:flex-nowrap gap-3 shrink-0">
                <button onclick="openLanguageModal('python')" class="px-5 py-3 rounded-xl bg-white text-navy-950 font-bold text-sm hover:bg-indigo-50 transition shadow-lg flex items-center gap-2">
                  <span>Continue Python</span>
                  <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2.2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M13 7l5 5m0 0l-5 5m5-5H6"/></svg>
                </button>
                <button onclick="navigateTo('performance')" class="px-5 py-3 rounded-xl bg-white/10 hover:bg-white/15 border border-white/20 text-white font-semibold text-sm transition">
                  View Analytics
                </button>
              </div>
            </div>
          </div>

          <!-- 4 Key KPI Stat Cards -->
          <div class="grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-4 gap-5">
            <!-- Total Quizzes Attempted -->
            <div class="glass-card glass-card-hover rounded-2xl p-5">
              <div class="flex items-start justify-between">
                <div>
                  <p class="text-xs font-semibold uppercase tracking-wider text-slate-400">Quizzes Attempted</p>
                  <h3 id="statTotalQuizzes" class="text-3xl font-extrabold text-white mt-2">27</h3>
                </div>
                <div class="w-11 h-11 rounded-xl bg-purple-500/20 border border-purple-500/30 flex items-center justify-center text-purple-400">
                  <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-6 9l2 2 4-4"/></svg>
                </div>
              </div>
              <div class="mt-4 flex items-center gap-2 text-xs">
                <span class="px-2 py-0.5 rounded-md bg-emerald-500/15 text-emerald-400 font-semibold">+5 this week</span>
                <span class="text-slate-400">Across 6 languages</span>
              </div>
            </div>

            <!-- Total Learning Time -->
            <div class="glass-card glass-card-hover rounded-2xl p-5">
              <div class="flex items-start justify-between">
                <div>
                  <p class="text-xs font-semibold uppercase tracking-wider text-slate-400">Total Learning Time</p>
                  <h3 id="statTotalTime" class="text-3xl font-extrabold text-white mt-2">20h 50m</h3>
                </div>
                <div class="w-11 h-11 rounded-xl bg-blue-500/20 border border-blue-500/30 flex items-center justify-center text-blue-400">
                  <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
                </div>
              </div>
              <div class="mt-4 flex items-center gap-2 text-xs">
                <span class="px-2 py-0.5 rounded-md bg-blue-500/15 text-blue-300 font-semibold">48m daily avg</span>
                <span class="text-slate-400">Active practice</span>
              </div>
            </div>

            <!-- Overall Improvement -->
            <div class="glass-card glass-card-hover rounded-2xl p-5">
              <div class="flex items-start justify-between">
                <div>
                  <p class="text-xs font-semibold uppercase tracking-wider text-slate-400">Overall Improvement</p>
                  <h3 id="statImprovement" class="text-3xl font-extrabold text-emerald-400 mt-2">+28.5%</h3>
                </div>
                <div class="w-11 h-11 rounded-xl bg-emerald-500/20 border border-emerald-500/30 flex items-center justify-center text-emerald-400">
                  <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"/></svg>
                </div>
              </div>
              <div class="mt-4 flex items-center gap-2 text-xs">
                <span class="px-2 py-0.5 rounded-md bg-emerald-500/15 text-emerald-400 font-semibold">Top 12%</span>
                <span class="text-slate-400">Since diagnostic test</span>
              </div>
            </div>

            <!-- Average Quiz Accuracy -->
            <div class="glass-card glass-card-hover rounded-2xl p-5">
              <div class="flex items-start justify-between">
                <div>
                  <p class="text-xs font-semibold uppercase tracking-wider text-slate-400">Average Accuracy</p>
                  <h3 id="statAvgAccuracy" class="text-3xl font-extrabold text-white mt-2">84.2%</h3>
                </div>
                <div class="w-11 h-11 rounded-xl bg-cyan-500/20 border border-cyan-500/30 flex items-center justify-center text-cyan-400">
                  <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 12l2 2 4-4M7.835 4.697a3.42 3.42 0 001.946-.806 3.42 3.42 0 014.438 0 3.42 3.42 0 001.946.806 3.42 3.42 0 013.138 3.138 3.42 3.42 0 00.806 1.946 3.42 3.42 0 010 4.438 3.42 3.42 0 00-.806 1.946 3.42 3.42 0 01-3.138 3.138 3.42 3.42 0 00-1.946.806 3.42 3.42 0 01-4.438 0 3.42 3.42 0 00-1.946-.806 3.42 3.42 0 01-3.138-3.138 3.42 3.42 0 00-.806-1.946 3.42 3.42 0 010-4.438 3.42 3.42 0 00.806-1.946 3.42 3.42 0 013.138-3.138z"/></svg>
                </div>
              </div>
              <div class="mt-4 flex items-center gap-2 text-xs">
                <span class="px-2 py-0.5 rounded-md bg-cyan-500/15 text-cyan-300 font-semibold">114 / 135</span>
                <span class="text-slate-400">Questions solved</span>
              </div>
            </div>
          </div>

          <!-- Charts & Language Mastery Row -->
          <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <!-- Weekly Quiz Performance Chart -->
            <div class="lg:col-span-2 glass-card rounded-2xl p-6 flex flex-col justify-between">
              <div class="flex flex-wrap items-center justify-between gap-2 mb-4">
                <div>
                  <h3 class="text-base font-bold text-white">Quiz Performance &amp; Learning Velocity</h3>
                  <p class="text-xs text-slate-400">Score percentage and study minutes over the last 7 sessions</p>
                </div>
                <span class="px-3 py-1 rounded-lg bg-purple-500/15 border border-purple-500/25 text-xs font-semibold text-purple-300">Live Telemetry</span>
              </div>
              <div class="relative h-64 w-full">
                <canvas id="dashboardActivityChart"></canvas>
              </div>
            </div>

            <!-- Language Mastery Progress Bars -->
            <div class="glass-card rounded-2xl p-6 flex flex-col justify-between">
              <div>
                <div class="flex items-center justify-between mb-4">
                  <h3 class="text-base font-bold text-white">Language Mastery</h3>
                  <button onclick="navigateTo('languages')" class="text-xs font-semibold text-purple-400 hover:text-purple-300">All Tracks →</button>
                </div>
                <div id="dashboardLanguageBars" class="space-y-4"></div>
              </div>
              <div class="mt-5 pt-4 border-t border-indigo-500/15 flex items-center justify-between text-xs text-slate-400">
                <span>Unlock Level 3 by scoring ≥60%</span>
                <span class="text-indigo-300 font-semibold">6 Active Tracks</span>
              </div>
            </div>
          </div>

          <!-- Recently Attempted Quizzes -->
          <div class="glass-card rounded-2xl p-6">
            <div class="flex flex-wrap items-center justify-between gap-3 mb-5">
              <div>
                <h3 class="text-base font-bold text-white">Recently Attempted Quizzes</h3>
                <p class="text-xs text-slate-400">Your latest quiz submissions, accuracy scores, and completion timestamps</p>
              </div>
              <button onclick="navigateTo('performance')" class="px-3.5 py-1.5 rounded-xl bg-navy-800 hover:bg-navy-700 border border-indigo-500/25 text-xs font-semibold text-indigo-200 transition">
                Full History
              </button>
            </div>
            <div class="overflow-x-auto">
              <table class="w-full text-left border-collapse">
                <thead>
                  <tr class="border-b border-indigo-500/20 text-[11px] font-semibold uppercase tracking-wider text-slate-400">
                    <th class="pb-3 pr-4">Language</th>
                    <th class="pb-3 px-4">Difficulty Level</th>
                    <th class="pb-3 px-4">Score</th>
                    <th class="pb-3 px-4">Accuracy</th>
                    <th class="pb-3 px-4">Time Spent</th>
                    <th class="pb-3 pl-4 text-right">Action</th>
                  </tr>
                </thead>
                <tbody id="recentQuizzesTableBody" class="divide-y divide-indigo-500/10 text-sm"></tbody>
              </table>
            </div>
          </div>
        </section>

        <!-- ==================== VIEW 2: LANGUAGES & LEVELS ==================== -->
        <section id="view-languages" class="hidden space-y-6 fade-in">
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div>
              <h2 class="text-2xl font-extrabold text-white">Programming Languages</h2>
              <p class="text-sm text-slate-400 mt-1">Select a language track to unlock progressive difficulty tiers from Basics to Advanced.</p>
            </div>
            <div class="flex items-center gap-2 text-xs bg-navy-800/90 border border-indigo-500/25 px-4 py-2.5 rounded-xl text-indigo-200">
              <span>🔓</span>
              <span>Score <strong>60% or higher</strong> on a level to unlock the next tier</span>
            </div>
          </div>

          <!-- Language Cards Grid -->
          <div id="languageCardsGrid" class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-6"></div>
        </section>

        <!-- ==================== VIEW 3: QUIZ ARENA ==================== -->
        <section id="view-quiz" class="hidden space-y-6 fade-in">
          <!-- Quiz Active Container -->
          <div id="quizActivePanel" class="max-w-3xl mx-auto">
            <!-- Top Quiz Meta Bar -->
            <div class="glass-card rounded-2xl p-4 sm:p-5 mb-5 flex flex-wrap items-center justify-between gap-4">
              <div class="flex items-center gap-3">
                <div id="quizLangBadge" class="w-11 h-11 rounded-xl bg-purple-500/20 border border-purple-500/30 flex items-center justify-center font-bold text-white">
                  PY
                </div>
                <div>
                  <div class="flex items-center gap-2">
                    <h2 id="quizHeaderTitle" class="text-base sm:text-lg font-bold text-white">Python • Level 1</h2>
                    <span id="quizLevelTag" class="px-2.5 py-0.5 rounded-full text-[11px] font-semibold bg-blue-500/20 text-blue-300 border border-blue-500/30">Basics</span>
                  </div>
                  <p id="quizQuestionCounter" class="text-xs text-slate-400 mt-0.5">Question 1 of 5</p>
                </div>
              </div>

              <div class="flex items-center gap-3">
                <div class="px-3.5 py-2 rounded-xl bg-navy-950/90 border border-indigo-500/25 flex items-center gap-2">
                  <svg class="w-4 h-4 text-purple-400" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
                  <span id="quizTimerDisplay" class="font-mono text-sm font-bold text-white">00:00</span>
                </div>
                <button onclick="exitQuizConfirm()" class="px-3 py-2 rounded-xl bg-rose-500/15 hover:bg-rose-500/25 border border-rose-500/30 text-rose-300 text-xs font-semibold transition">
                  Exit
                </button>
              </div>
            </div>

            <!-- Progress Bar -->
            <div class="mb-6">
              <div class="flex justify-between text-xs font-medium text-slate-400 mb-2">
                <span>Quiz Progress</span>
                <span id="quizProgressPercent" class="text-purple-300 font-mono">20%</span>
              </div>
              <div class="w-full h-2.5 bg-navy-800 rounded-full overflow-hidden border border-indigo-500/20">
                <div id="quizProgressBar" class="h-full bg-gradient-to-r from-purple-500 via-indigo-500 to-blue-400 rounded-full transition-all duration-500" style="width: 20%"></div>
              </div>
            </div>

            <!-- Question Card -->
            <div class="glass-card rounded-3xl p-6 sm:p-8 space-y-6">
              <div>
                <span class="inline-block px-3 py-1 rounded-lg bg-indigo-500/15 border border-indigo-500/25 text-indigo-300 text-xs font-mono mb-3" id="quizTopicTag">
                  Core Syntax &amp; Concepts
                </span>
                <h3 id="quizQuestionText" class="text-lg sm:text-xl font-bold text-white leading-snug">
                  Loading question...
                </h3>
                <!-- Optional Code Snippet -->
                <pre id="quizCodeBlock" class="hidden mt-4 p-4 rounded-2xl bg-navy-950/95 border border-indigo-500/25 font-mono text-xs sm:text-sm text-cyan-300 overflow-x-auto leading-relaxed"></pre>
              </div>

              <!-- 4 Answer Options -->
              <div id="quizOptionsContainer" class="space-y-3"></div>

              <!-- Instant Feedback Banner -->
              <div id="quizFeedbackBox" class="hidden rounded-2xl p-4 border text-sm transition-all">
                <div class="flex items-start gap-3">
                  <span id="quizFeedbackIcon" class="text-xl mt-0.5">✅</span>
                  <div>
                    <p id="quizFeedbackTitle" class="font-bold"></p>
                    <p id="quizFeedbackExplanation" class="text-xs sm:text-sm mt-1 opacity-90"></p>
                  </div>
                </div>
              </div>

              <!-- Bottom Navigation -->
              <div class="pt-2 flex items-center justify-between border-t border-indigo-500/15">
                <div class="text-xs text-slate-400">
                  Current Score: <span id="quizLiveScore" class="font-bold text-white">0</span> / <span id="quizTotalQ">5</span>
                </div>
                <button id="nextQuestionBtn" onclick="handleNextQuestion()" disabled class="gradient-btn disabled:opacity-40 disabled:pointer-events-none px-6 py-3 rounded-xl text-sm font-bold text-white flex items-center gap-2 shadow-lg">
                  <span id="nextQuestionBtnText">Next Question</span>
                  <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2.2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M13 7l5 5m0 0l-5 5m5-5H6"/></svg>
                </button>
              </div>
            </div>
          </div>

          <!-- Quiz Completion Result Card -->
          <div id="quizResultPanel" class="hidden max-w-2xl mx-auto glass-card rounded-3xl p-6 sm:p-10 text-center space-y-6 fade-in">
            <div id="resultBadgeIcon" class="w-20 h-20 mx-auto rounded-2xl bg-gradient-to-br from-purple-500 to-blue-500 flex items-center justify-center text-4xl shadow-xl shadow-purple-600/30">
              🏆
            </div>
            <div>
              <span id="resultStatusPill" class="px-3.5 py-1 rounded-full text-xs font-bold uppercase tracking-wider bg-emerald-500/20 text-emerald-300 border border-emerald-500/30">
                Level Cleared!
              </span>
              <h2 id="resultHeadline" class="text-2xl sm:text-3xl font-extrabold text-white mt-3">Outstanding Performance!</h2>
              <p id="resultSubtext" class="text-sm text-slate-300 mt-1">You mastered Python Level 1 and unlocked Level 2 – Intermediate.</p>
            </div>

            <!-- Score Breakdown -->
            <div class="grid grid-cols-3 gap-3 sm:gap-4 pt-2">
              <div class="p-4 rounded-2xl bg-navy-950/80 border border-indigo-500/20">
                <p class="text-xs text-slate-400">Final Score</p>
                <p id="resultScoreValue" class="text-xl sm:text-2xl font-extrabold text-white mt-1">5 / 5</p>
              </div>
              <div class="p-4 rounded-2xl bg-navy-950/80 border border-indigo-500/20">
                <p class="text-xs text-slate-400">Accuracy</p>
                <p id="resultAccuracyValue" class="text-xl sm:text-2xl font-extrabold text-emerald-400 mt-1">100%</p>
              </div>
              <div class="p-4 rounded-2xl bg-navy-950/80 border border-indigo-500/20">
                <p class="text-xs text-slate-400">Time Taken</p>
                <p id="resultTimeValue" class="text-xl sm:text-2xl font-extrabold text-blue-400 mt-1">01:14</p>
              </div>
            </div>

            <div id="resultUnlockNotice" class="hidden p-4 rounded-2xl bg-gradient-to-r from-purple-500/20 to-blue-500/20 border border-purple-400/30 text-sm text-purple-100 font-medium">
              🔓 <strong>New Level Unlocked:</strong> You can now challenge the next difficulty tier!
            </div>

            <div class="flex flex-wrap items-center justify-center gap-3 pt-2">
              <button id="resultNextLevelBtn" onclick="startNextUnlockedLevel()" class="gradient-btn px-6 py-3 rounded-xl text-sm font-bold text-white shadow-lg">
                Start Next Level →
              </button>
              <button onclick="retakeCurrentQuiz()" class="px-5 py-3 rounded-xl bg-navy-800 hover:bg-navy-700 border border-indigo-500/30 text-sm font-semibold text-white transition">
                Retry Quiz
              </button>
              <button onclick="navigateTo('dashboard')" class="px-5 py-3 rounded-xl bg-white/5 hover:bg-white/10 text-sm font-semibold text-slate-300 transition">
                Back to Dashboard
              </button>
            </div>
          </div>
        </section>

        <!-- ==================== VIEW 4: PERFORMANCE ANALYTICS ==================== -->
        <section id="view-performance" class="hidden space-y-6 fade-in">
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div>
              <h2 class="text-2xl font-extrabold text-white">Performance &amp; Progress Analytics</h2>
              <p class="text-sm text-slate-400 mt-1">Deep insights into time investment, language-wise accuracy, and historical quiz trends.</p>
            </div>
            <div class="flex items-center gap-2">
              <span class="px-3.5 py-2 rounded-xl bg-emerald-500/15 border border-emerald-500/30 text-emerald-300 text-xs font-bold">
                Overall Growth: <span id="perfOverallGrowth">+28.5%</span>
              </span>
            </div>
          </div>

          <!-- Top Analytics Summary Grid -->
          <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
            <!-- Time Spent Per Language Doughnut Chart -->
            <div class="glass-card rounded-2xl p-6">
              <div class="mb-4">
                <h3 class="text-base font-bold text-white">Time Spent by Programming Language</h3>
                <p class="text-xs text-slate-400">Distribution of your <span id="perfTotalTimeInline" class="text-white font-semibold">20h 50m</span> total learning time</p>
              </div>
              <div class="grid grid-cols-1 sm:grid-cols-2 items-center gap-4">
                <div class="relative h-56">
                  <canvas id="languageTimeChart"></canvas>
                </div>
                <div id="languageTimeLegend" class="space-y-2.5"></div>
              </div>
            </div>

            <!-- Accuracy Progression Line Chart -->
            <div class="glass-card rounded-2xl p-6">
              <div class="mb-4">
                <h3 class="text-base font-bold text-white">Score &amp; Accuracy Trend</h3>
                <p class="text-xs text-slate-400">Chronological improvement across completed assessments</p>
              </div>
              <div class="relative h-56">
                <canvas id="accuracyTrendChart"></canvas>
              </div>
            </div>
          </div>

          <!-- Language-Wise Progress Cards -->
          <div class="glass-card rounded-2xl p-6">
            <h3 class="text-base font-bold text-white mb-4">Language-Wise Breakdown</h3>
            <div id="perfLanguageCards" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-6 gap-4"></div>
          </div>

          <!-- Complete Previous Quiz Performance Log -->
          <div class="glass-card rounded-2xl p-6">
            <div class="flex flex-wrap items-center justify-between gap-3 mb-4">
              <div>
                <h3 class="text-base font-bold text-white">Previous Quiz Performance Log</h3>
                <p class="text-xs text-slate-400">Detailed record of all attempted quizzes across languages and levels</p>
              </div>
              <div class="flex flex-wrap gap-2" id="perfFilterPills">
                <button onclick="filterHistory('all')" class="filter-pill active-pill px-3 py-1.5 rounded-lg text-xs font-semibold bg-purple-600 text-white">All</button>
                <button onclick="filterHistory('c')" class="filter-pill px-3 py-1.5 rounded-lg text-xs font-semibold bg-navy-800 text-slate-300 hover:text-white">C</button>
                <button onclick="filterHistory('cpp')" class="filter-pill px-3 py-1.5 rounded-lg text-xs font-semibold bg-navy-800 text-slate-300 hover:text-white">C++</button>
                <button onclick="filterHistory('java')" class="filter-pill px-3 py-1.5 rounded-lg text-xs font-semibold bg-navy-800 text-slate-300 hover:text-white">Java</button>
                <button onclick="filterHistory('python')" class="filter-pill px-3 py-1.5 rounded-lg text-xs font-semibold bg-navy-800 text-slate-300 hover:text-white">Python</button>
                <button onclick="filterHistory('javascript')" class="filter-pill px-3 py-1.5 rounded-lg text-xs font-semibold bg-navy-800 text-slate-300 hover:text-white">JavaScript</button>
                <button onclick="filterHistory('css')" class="filter-pill px-3 py-1.5 rounded-lg text-xs font-semibold bg-navy-800 text-slate-300 hover:text-white">CSS</button>
              </div>
            </div>
            <div class="overflow-x-auto">
              <table class="w-full text-left border-collapse">
                <thead>
                  <tr class="border-b border-indigo-500/20 text-[11px] font-semibold uppercase tracking-wider text-slate-400">
                    <th class="pb-3 pr-4">Date</th>
                    <th class="pb-3 px-4">Language</th>
                    <th class="pb-3 px-4">Level</th>
                    <th class="pb-3 px-4">Score</th>
                    <th class="pb-3 px-4">Accuracy</th>
                    <th class="pb-3 pl-4 text-right">Duration</th>
                  </tr>
                </thead>
                <tbody id="fullHistoryTableBody" class="divide-y divide-indigo-500/10 text-sm"></tbody>
              </table>
            </div>
          </div>
        </section>

      </main>
    </div>
  </div>

  <!-- ==================== MODAL: LANGUAGE LEVEL SELECTOR ==================== -->
  <div id="levelSelectModal" class="fixed inset-0 z-50 hidden items-center justify-center p-4 bg-black/75 backdrop-blur-md">
    <div class="glass-card rounded-3xl max-w-xl w-full p-6 sm:p-8 border border-purple-500/35 shadow-2xl fade-in relative">
      <button onclick="closeLevelModal()" class="absolute top-5 right-5 w-9 h-9 rounded-xl bg-white/5 hover:bg-white/10 flex items-center justify-center text-slate-300 hover:text-white transition">
        ✕
      </button>

      <div class="flex items-center gap-4 mb-6">
        <div id="modalLangIcon" class="w-14 h-14 rounded-2xl flex items-center justify-center shadow-lg"></div>
        <div>
          <span class="text-xs font-semibold uppercase tracking-wider text-purple-300">Select Learning Tier</span>
          <h3 id="modalLangName" class="text-2xl font-extrabold text-white">Python</h3>
          <p id="modalLangStats" class="text-xs text-slate-400 mt-0.5">Progress: 67% • Time Spent: 5h 20m</p>
        </div>
      </div>

      <div id="modalLevelsList" class="space-y-3.5"></div>

      <div class="mt-6 pt-4 border-t border-indigo-500/15 flex items-center justify-between text-xs text-slate-400">
        <span>Passing criteria: 3/5 correct answers (60%)</span>
        <button onclick="closeLevelModal()" class="text-slate-300 hover:text-white font-semibold">Close</button>
      </div>
    </div>
  </div>

  <script>
    // =========================================================================
    // 1. SAMPLE DATA & COMPREHENSIVE QUESTION BANK (C, C++, JAVA, PYTHON, JS, CSS)
    // =========================================================================
    const LANGUAGES = {
      c: {
        id: 'c',
        name: 'C',
        short: 'C',
        tagline: 'Procedural Systems & Memory Control',
        color: '#3B82F6',
        gradient: 'from-blue-600 to-cyan-500',
        badgeBg: 'bg-blue-500/20 text-blue-300 border-blue-500/30',
        timeMinutes: 230, // 3h 50m
        unlockedLevel: 2,
        completedLevels: [1],
        accuracy: 82,
        icon: `<svg viewBox="0 0 24 24" class="w-7 h-7" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2L3 7v10l9 5 9-5V7l-9-5z" stroke="#60A5FA"/><path d="M15.5 9.5a4.5 4.5 0 100 5" stroke="#93C5FD" stroke-width="2.4" stroke-linecap="round"/></svg>`
      },
      cpp: {
        id: 'cpp',
        name: 'C++',
        short: 'C++',
        tagline: 'Object-Oriented & High-Performance STL',
        color: '#8B5CF6',
        gradient: 'from-indigo-600 to-purple-500',
        badgeBg: 'bg-indigo-500/20 text-indigo-300 border-indigo-500/30',
        timeMinutes: 265, // 4h 25m
        unlockedLevel: 2,
        completedLevels: [1],
        accuracy: 80,
        icon: `<svg viewBox="0 0 24 24" class="w-7 h-7" fill="none"><path d="M12 2L3 7v10l9 5 9-5V7l-9-5z" stroke="#A78BFA" stroke-width="2"/><path d="M11 9.5a3.5 3.5 0 100 5" stroke="#DDD6FE" stroke-width="2.2" stroke-linecap="round"/><path d="M15 12h3M16.5 10.5v3M19 12h2M20 11v2" stroke="#C4B5FD" stroke-width="1.8" stroke-linecap="round"/></svg>`
      },
      java: {
        id: 'java',
        name: 'Java',
        short: 'JV',
        tagline: 'Enterprise OOP & JVM Architecture',
        color: '#F59E0B',
        gradient: 'from-amber-500 to-orange-600',
        badgeBg: 'bg-amber-500/20 text-amber-300 border-amber-500/30',
        timeMinutes: 195, // 3h 15m
        unlockedLevel: 1,
        completedLevels: [],
        accuracy: 78,
        icon: `<svg viewBox="0 0 24 24" class="w-7 h-7" fill="none"><path d="M6 15h10a2 2 0 002-2v-2H6v4z" stroke="#FBBF24" stroke-width="2"/><path d="M18 11h1.5a1.5 1.5 0 010 3H18" stroke="#F59E0B" stroke-width="2"/><path d="M4 18h14" stroke="#FDE68A" stroke-width="2" stroke-linecap="round"/><path d="M9 7c0-1.5 2-1.5 2-3M13 7c0-1.5 2-1.5 2-3" stroke="#FBBF24" stroke-width="1.8" stroke-linecap="round"/></svg>`
      },
      python: {
        id: 'python',
        name: 'Python',
        short: 'PY',
        tagline: 'Data Structures, Scripting & AI Foundations',
        color: '#10B981',
        gradient: 'from-emerald-500 to-teal-600',
        badgeBg: 'bg-emerald-500/20 text-emerald-300 border-emerald-500/30',
        timeMinutes: 320, // 5h 20m
        unlockedLevel: 3,
        completedLevels: [1, 2],
        accuracy: 91,
        icon: `<svg viewBox="0 0 24 24" class="w-7 h-7" fill="none"><path d="M12 3c-3 0-3 1.5-3 3v2h6v1H7c-2 0-3 1.5-3 3.5S5 16 7 16h2v-2c0-1.5 1-2.5 2.5-2.5h4c1.5 0 2.5-1 2.5-2.5V6c0-1.5-1-3-3-3h-3z" stroke="#34D399" stroke-width="1.9"/><path d="M12 21c3 0 3-1.5 3-3v-2H9v-1h8c2 0 3-1.5 3-3.5S19 8 17 8h-2v2c0 1.5-1 2.5-2.5 2.5h-4C7 12.5 6 13.5 6 15v3c0 1.5 1 3 3 3h3z" stroke="#6EE7B7" stroke-width="1.9"/></svg>`
      },
      javascript: {
        id: 'javascript',
        name: 'JavaScript',
        short: 'JS',
        tagline: 'Modern ES6+, Async Event Loop & DOM',
        color: '#EC4899',
        gradient: 'from-pink-500 to-purple-600',
        badgeBg: 'bg-pink-500/20 text-pink-300 border-pink-500/30',
        timeMinutes: 110, // 1h 50m
        unlockedLevel: 2,
        completedLevels: [1],
        accuracy: 85,
        icon: `<svg viewBox="0 0 24 24" class="w-7 h-7" fill="none"><rect x="3" y="3" width="18" height="18" rx="4" stroke="#F472B6" stroke-width="2"/><path d="M10 9v6a2 2 0 01-2 2H7M14 15.5c.5.8 1.3 1.2 2.2 1.2 1.2 0 2-.6 2-1.5 0-1-.8-1.4-2-1.8-1.1-.4-1.9-.8-1.9-1.8 0-.9.8-1.6 1.9-1.6.9 0 1.6.4 2 1" stroke="#FBCFE8" stroke-width="1.9" stroke-linecap="round"/></svg>`
      },
      css: {
        id: 'css',
        name: 'CSS',
        short: 'CSS',
        tagline: 'Modern Layouts, Flexbox, Grid & Animations',
        color: '#06B6D4',
        gradient: 'from-cyan-500 to-blue-600',
        badgeBg: 'bg-cyan-500/20 text-cyan-300 border-cyan-500/30',
        timeMinutes: 130, // 2h 10m
        unlockedLevel: 1,
        completedLevels: [],
        accuracy: 86,
        icon: `<svg viewBox="0 0 24 24" class="w-7 h-7" fill="none"><path d="M4 3h16l-1.5 15.5L12 21l-6.5-2.5L4 3z" stroke="#22D3EE" stroke-width="2" stroke-linejoin="round"/><path d="M8 8h8l-.5 4H9.5l.3 3 2.2.8 2.2-.8.2-1.5" stroke="#A5F3FC" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round"/></svg>`
      }
    };

    const LEVEL_META = {
      1: { name: 'Level 1 – Basics', badge: 'Basics', desc: 'Syntax, data types, operators & fundamental control flow.' },
      2: { name: 'Level 2 – Intermediate', badge: 'Intermediate', desc: 'Functions, memory/references, collections & modular design.' },
      3: { name: 'Level 3 – Advanced', badge: 'Advanced', desc: 'Concurrency, optimization, internals & complex edge cases.' }
    };

    const QUESTION_BANK = {
      c: {
        1: [
          {
            topic: 'Data Types & Format Specifiers',
            q: 'Which format specifier is used to print a double-precision floating-point value using printf() in C?',
            code: '#include <stdio.h>\nint main() {\n    double pi = 3.14159;\n    printf("___", pi);\n    return 0;\n}',
            options: ['%d', '%lf', '%c', '%s'],
            answer: 1,
            explanation: '%lf (or %f in printf) formats double-precision floating-point numbers, whereas %d is for integers and %c is for characters.'
          },
          {
            topic: 'Operators & Precedence',
            q: 'What is the output of the following C code snippet?',
            code: 'int a = 10, b = 3;\nprintf("%d", a % b + a / b);',
            options: ['4', '3', '1', '6'],
            answer: 0,
            explanation: '10 % 3 evaluates to 1 (remainder), and integer division 10 / 3 evaluates to 3. Their sum is 1 + 3 = 4.'
          },
          {
            topic: 'Control Flow',
            q: 'Which loop in C is guaranteed to execute its body at least once even if the condition is initially false?',
            options: ['for loop', 'while loop', 'do-while loop', 'nested if'],
            answer: 2,
            explanation: 'A do-while loop checks its condition after executing the loop body, ensuring at least one execution.'
          },
          {
            topic: 'Storage & Constants',
            q: 'Which keyword is used in C to define a variable whose value cannot be modified after initialization?',
            options: ['static', 'const', 'extern', 'volatile'],
            answer: 1,
            explanation: 'The const qualifier instructs the compiler to prevent any modification to the variable after initialization.'
          },
          {
            topic: 'Arrays',
            q: 'What is the index of the last element in a C array declared as int arr[10];?',
            options: ['10', '9', '8', '0'],
            answer: 1,
            explanation: 'C uses zero-based indexing, so an array of size 10 has valid indices from 0 through 9.'
          }
        ],
        2: [
          {
            topic: 'Pointers',
            q: 'What does the dereference operator (*) do when applied to a pointer variable ptr?',
            code: 'int x = 42;\nint *ptr = &x;\nprintf("%d", *ptr);',
            options: ['Prints the memory address of ptr', 'Accesses the value stored at the address held by ptr', 'Declares a new pointer', 'Frees allocated heap memory'],
            answer: 1,
            explanation: '*ptr dereferences the pointer, retrieving the integer value 42 stored at the memory address of x.'
          },
          {
            topic: 'Dynamic Memory Allocation',
            q: 'Which standard library function allocates memory on the heap and initializes all bytes to zero?',
            options: ['malloc()', 'calloc()', 'realloc()', 'free()'],
            answer: 1,
            explanation: 'calloc(num, size) allocates memory for an array of elements and zero-initializes every byte, unlike malloc().'
          },
          {
            topic: 'Strings in C',
            q: 'Every standard C-style string must end with which special character?',
            options: ['\\n', '\\t', '\\0', 'EOF'],
            answer: 2,
            explanation: 'C strings are null-terminated character arrays ending with the null character \\0.'
          },
          {
            topic: 'Structures & Unions',
            q: 'How does a union differ from a struct in C?',
            options: ['Unions cannot hold integers', 'All members of a union share the same memory location', 'Structs cannot contain pointers', 'Unions allocate separate memory for each member'],
            answer: 1,
            explanation: 'In a union, all members share the exact same memory block, sized to the largest member.'
          },
          {
            topic: 'Pointer Arithmetic',
            q: 'If int *p points to address 1000 and sizeof(int) is 4 bytes, what address does p + 2 point to?',
            options: ['1002', '1004', '1008', '1016'],
            answer: 2,
            explanation: 'Pointer arithmetic scales by the size of the pointed type: 1000 + (2 * 4) = 1008.'
          }
        ],
        3: [
          {
            topic: 'Memory Pitfalls',
            q: 'What is a "dangling pointer" in C?',
            options: ['A pointer initialized to NULL', 'A pointer referencing memory that has already been freed', 'A pointer to a const variable', 'A void pointer'],
            answer: 1,
            explanation: 'A dangling pointer still holds the address of deallocated memory after free() is called, causing undefined behavior if dereferenced.'
          },
          {
            topic: 'Function Pointers',
            q: 'Which declaration correctly defines a pointer to a function taking two ints and returning an int?',
            options: ['int *func(int, int);', 'int (*func)(int, int);', 'int (func*)(int, int);', 'void (*func)(int, int);'],
            answer: 1,
            explanation: 'Parentheses around (*func) are mandatory so it binds as a pointer to a function rather than a function returning an int*.'
          },
          {
            topic: 'Type Qualifiers',
            q: 'Why is the volatile keyword used in embedded C programming?',
            options: ['To store variables in CPU registers', 'To prevent compiler optimizations on variables modified externally (e.g., hardware interrupts)', 'To speed up floating point math', 'To lock threads'],
            answer: 1,
            explanation: 'volatile forces the compiler to read the variable directly from memory every time rather than caching it in a register.'
          },
          {
            topic: 'Bitwise Operations',
            q: 'Which bitwise expression clears the k-th bit (0-indexed) of an integer n?',
            options: ['n | (1 << k)', 'n & ~(1 << k)', 'n ^ (1 << k)', 'n >> k'],
            answer: 1,
            explanation: '~(1 << k) creates a bitmask with 0 at position k and 1s elsewhere; ANDing it clears only bit k.'
          },
          {
            topic: 'Preprocessor Macros',
            q: 'What is the hidden bug in #define SQUARE(x) x * x when called as SQUARE(2 + 3)?',
            options: ['Compilation syntax error', 'Expands to 2 + 3 * 2 + 3 = 11 instead of 25', 'Integer overflow', 'Returns 0'],
            answer: 1,
            explanation: 'Macros perform textual substitution without parentheses: 2 + 3 * 2 + 3 evaluates 3*2 first, yielding 11.'
          }
        ]
      },
      cpp: {
        1: [
          {
            topic: 'I/O Streams',
            q: 'Which header file is required to use std::cout and std::cin in C++?',
            options: ['<stdio.h>', '<iostream>', '<fstream>', '<sstream>'],
            answer: 1,
            explanation: '<iostream> defines the standard input/output stream objects std::cin and std::cout.'
          },
          {
            topic: 'References',
            q: 'What is true about a reference variable in C++ (e.g., int& ref = x;)?',
            options: ['It can be NULL', 'It must be initialized when declared and acts as an alias', 'It can be reassigned to another variable later', 'It requires -> to access members'],
            answer: 1,
            explanation: 'C++ references must be bound at initialization and cannot be reseated to refer to another object.'
          },
          {
            topic: 'OOP Basics',
            q: 'What is the default access specifier for members inside a C++ class?',
            options: ['public', 'protected', 'private', 'internal'],
            answer: 2,
            explanation: 'Unlike struct (which defaults to public), class members in C++ default to private access.'
          },
          {
            topic: 'Namespaces',
            q: 'What does the scope resolution operator (::) do in std::vector?',
            options: ['Dereferences a pointer', 'Specifies that vector belongs to the std namespace', 'Performs bitwise OR', 'Calls a destructor'],
            answer: 1,
            explanation: 'The :: operator resolves identifiers inside a specific namespace or class scope.'
          },
          {
            topic: 'Function Overloading',
            q: 'C++ allows multiple functions to share the same name provided they differ in:',
            options: ['Return type only', 'Parameter types or number of parameters', 'Variable names inside the body', 'Access specifiers'],
            answer: 1,
            explanation: 'Function overloading is resolved by parameter list signature (count, types, or const-qualification), not return type alone.'
          }
        ],
        2: [
          {
            topic: 'STL Containers',
            q: 'Which STL container stores unique keys in sorted order with O(log n) lookup time?',
            options: ['std::vector', 'std::unordered_map', 'std::set', 'std::queue'],
            answer: 2,
            explanation: 'std::set is typically implemented as a Red-Black Tree, maintaining unique elements in sorted order with O(log n) operations.'
          },
          {
            topic: 'Polymorphism',
            q: 'Which keyword enables dynamic (runtime) polymorphism for a member function in a base class?',
            options: ['inline', 'virtual', 'friend', 'explicit'],
            answer: 1,
            explanation: 'Marking a base class method virtual uses the vtable so derived overrides are invoked via base pointers/references.'
          },
          {
            topic: 'Constructors & Destructors',
            q: 'Why should a base class with virtual functions always declare a virtual destructor?',
            options: ['To improve loop speed', 'To ensure the derived class destructor runs when deleting via a base pointer', 'To prevent inheritance', 'To overload new'],
            answer: 1,
            explanation: 'Without a virtual destructor, deleting a derived object through a base pointer causes undefined behavior and resource leaks.'
          },
          {
            topic: 'Modern C++ Type Deduction',
            q: 'What type does auto deduce for x in: const int a = 10; auto x = a;?',
            options: ['const int', 'int', 'int&', 'const int*'],
            answer: 1,
            explanation: 'By-value auto deduction strips top-level const and references, deducing x as a plain modifiable int.'
          },
          {
            topic: 'Vector Complexity',
            q: 'What is the amortized time complexity of std::vector::push_back()?',
            options: ['O(1)', 'O(log n)', 'O(n)', 'O(n log n)'],
            answer: 0,
            explanation: 'Because std::vector grows geometrically (typically doubling capacity), push_back runs in O(1) amortized time.'
          }
        ],
        3: [
          {
            topic: 'Smart Pointers & RAII',
            q: 'Which smart pointer enforces exclusive ownership and cannot be copied, only moved?',
            options: ['std::shared_ptr', 'std::weak_ptr', 'std::unique_ptr', 'std::auto_ptr'],
            answer: 2,
            explanation: 'std::unique_ptr enforces sole ownership via deleted copy constructors, supporting ownership transfer via std::move.'
          },
          {
            topic: 'Move Semantics',
            q: 'What does std::move(obj) actually do at runtime?',
            options: ['Copies bytes in memory', 'Casts obj to an rvalue reference so move constructors/assignments can be selected', 'Deletes obj immediately', 'Allocates heap storage'],
            answer: 1,
            explanation: 'std::move is purely an unconditional static_cast to an rvalue reference (T&&); actual resource transfer occurs in the move constructor.'
          },
          {
            topic: 'Templates & SFINAE',
            q: 'What does RAII stand for in C++ resource management?',
            options: ['Runtime Array Index Inspection', 'Resource Acquisition Is Initialization', 'Random Access Iterator Interface', 'Recursive Allocation In Inheritance'],
            answer: 1,
            explanation: 'RAII ties resource lifetimes (memory, file handles, mutexes) to object scope so destructors clean up automatically.'
          },
          {
            topic: 'Smart Pointer Cycles',
            q: 'How do you break cyclic references between two objects holding std::shared_ptr to each other?',
            options: ['Use raw int variables', 'Replace one side with std::weak_ptr', 'Call std::move twice', 'Use static_cast'],
            answer: 1,
            explanation: 'std::weak_ptr observes a shared_ptr-managed object without incrementing its strong reference count, preventing memory leaks.'
          },
          {
            topic: 'Lambda Captures',
            q: 'In C++, what does the lambda capture clause [&] signify?',
            options: ['Capture all local variables by value', 'Capture all used local variables by reference', 'Capture nothing', 'Capture global variables only'],
            answer: 1,
            explanation: '[&] implicitly captures all automatic variables referenced inside the lambda body by reference.'
          }
        ]
      },
      java: {
        1: [
          {
            topic: 'JVM & Compilation',
            q: 'What intermediate code does the Java compiler (javac) generate from .java source files?',
            options: ['Machine assembly', 'Platform-independent Bytecode (.class)', 'LLVM IR', 'C source code'],
            answer: 1,
            explanation: 'javac compiles Java source into bytecode (.class), which the JVM executes on any platform.'
          },
          {
            topic: 'Strings & Immutability',
            q: 'What is the output of the following Java comparison?',
            code: 'String s1 = new String("Codezilla");\nString s2 = new String("Codezilla");\nSystem.out.println(s1 == s2);',
            options: ['true', 'false', 'Compilation error', 'NullPointerException'],
            answer: 1,
            explanation: '== compares object references in Java. Two distinct new String() objects reside at different heap addresses, so s1 == s2 is false.'
          },
          {
            topic: 'Primitive Data Types',
            q: 'Which of the following is NOT a primitive data type in Java?',
            options: ['boolean', 'double', 'String', 'char'],
            answer: 2,
            explanation: 'String is a reference class in java.lang, whereas boolean, double, and char are built-in primitive types.'
          },
          {
            topic: 'Inheritance',
            q: 'Which keyword is used by a Java class to inherit from a superclass?',
            options: ['implements', 'extends', 'inherits', 'super'],
            answer: 1,
            explanation: 'A class uses extends to inherit from another class, and implements to adopt an interface.'
          },
          {
            topic: 'Entry Point',
            q: 'Why is the main() method declared static in Java?',
            options: ['So it cannot be overloaded', 'So the JVM can invoke it without instantiating the class first', 'To make variables thread-safe', 'To enable garbage collection'],
            answer: 1,
            explanation: 'Making main() static allows the JVM runtime to launch the program directly without creating an instance of the enclosing class.'
          }
        ],
        2: [
          {
            topic: 'Collections Framework',
            q: 'Which Java collection guarantees O(1) average lookup and does NOT allow duplicate keys?',
            options: ['ArrayList', 'LinkedList', 'HashMap', 'TreeSet'],
            answer: 2,
            explanation: 'HashMap hashes keys into buckets for O(1) average-time get/put operations while enforcing unique keys.'
          },
          {
            topic: 'Exception Handling',
            q: 'When does a finally block execute in a try-catch-finally statement?',
            options: ['Only when an exception is thrown', 'Only when no exception occurs', 'Always, regardless of whether an exception was thrown or caught', 'Only for unchecked exceptions'],
            answer: 2,
            explanation: 'The finally block always executes after try/catch exits (unless System.exit() is called), making it ideal for cleanup.'
          },
          {
            topic: 'Interfaces & Abstract Classes',
            q: 'Since Java 8, can an interface contain methods with concrete implementations?',
            options: ['No, never', 'Yes, using default or static methods', 'Only private constructors', 'Only if marked final'],
            answer: 1,
            explanation: 'Java 8 introduced default and static methods in interfaces to allow backward-compatible API evolution.'
          },
          {
            topic: 'StringBuilder vs String',
            q: 'Why is StringBuilder preferred over String concatenation inside a large loop?',
            options: ['StringBuilder is immutable', 'String is immutable, creating many temporary objects on the heap', 'StringBuilder uses less syntax', 'String throws IOException'],
            answer: 1,
            explanation: 'Because String objects are immutable, repeated + concatenation allocates a new String every iteration, whereas StringBuilder mutates an internal buffer.'
          },
          
