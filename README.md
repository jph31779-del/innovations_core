<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1.0" />
  <title>IFH | COMMAND_CORE</title>

  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">
  
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            vanta: '#050505',       /* Deepest Black */
            panel: '#0F0F0F',       /* Slightly Lighter Black */
            nickel: '#A1A1AA',      /* Metallic Text */
            alert: '#ef4444',       /* Red Status */
            success: '#10b981',     /* Green Status */
            hud: '#3b82f6',         /* Blue UI Accents */
          },
          fontFamily: {
            sans: ['Inter', 'sans-serif'],
            mono: ['JetBrains Mono', 'monospace'],
          }
        }
      }
    }
  </script>

  <style>
    body { font-family: "Inter", sans-serif; background-color: var(--vanta); color: var(--nickel); }
    /* Tactical Inputs */
    input, textarea { 
        background-color: #000; 
        border: 1px solid #333; 
        color: #fff; 
        font-family: "JetBrains Mono", monospace;
        transition: all 0.2s; 
    }
    input:focus, textarea:focus { outline: none; border-color: #3b82f6; }
    
    /* Scrollbar for raw JSON */
    ::-webkit-scrollbar { width: 8px; }
    ::-webkit-scrollbar-track { background: #000; }
    ::-webkit-scrollbar-thumb { background: #333; border-radius: 4px; }
    ::-webkit-scrollbar-thumb:hover { background: #555; }
  </style>
</head>

<body class="bg-vanta text-nickel min-h-screen">

  <nav class="bg-vanta border-b border-zinc-800 sticky top-0 z-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between h-16 items-center">
        <div class="flex items-center gap-3">
          <div class="w-3 h-3 bg-hud rounded-full animate-pulse"></div> <span class="text-lg font-bold text-gray-100 tracking-wider font-mono">
            INNOVATIONS_CORE
          </span>
          <span class="px-2 py-0.5 border border-zinc-700 text-zinc-400 text-[10px] font-mono uppercase tracking-widest">
            Restricted
          </span>
        </div>
        <div>
          <button id="btnExport"
            class="group bg-zinc-900 hover:bg-zinc-800 border border-zinc-700 text-gray-300 px-4 py-2 text-xs font-mono uppercase tracking-wide transition">
            <span class="text-hud group-hover:text-white mr-2">⇩</span>Export JSON
          </button>
        </div>
      </div>
    </div>
  </nav>

  <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">

    <header class="mb-8 flex flex-col sm:flex-row sm:items-end justify-between gap-4 border-b border-zinc-800 pb-6">
      <div>
        <h1 class="text-2xl font-bold text-white tracking-tight">OPERATIONAL STATUS</h1>
        <div class="mt-2 flex items-center gap-4 text-sm font-mono text-zinc-500">
           <span id="asOf">DATE: —</span>
           <span id="savedBadge" class="text-zinc-600">SYNC: —</span>
        </div>
      </div>
    </header>

    <section class="grid grid-cols-1 md:grid-cols-4 gap-4 mb-8 font-mono">
      <div class="bg-panel p-5 border border-zinc-800 border-l-4 border-l-
