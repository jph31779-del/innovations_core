#innovations-core<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1.0" />
  <title>Innovations From The Hart LLC | Mission Control</title>

  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
  <style>
    body { font-family: "Inter", sans-serif; }
    /* Smooth transitions for inputs */
    input, textarea { transition: all 0.2s; }
    input:focus, textarea:focus { outline: none; border-color: #4f46e5; ring: 2px; }
  </style>
</head>

<body class="bg-gray-100 text-gray-900">

  <nav class="bg-white border-b border-gray-200 sticky top-0 z-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between h-16 items-center">
        <div class="flex items-center gap-3">
          <span class="text-xl sm:text-2xl font-bold text-indigo-700 tracking-tight">
            Innovations From The Hart LLC
          </span>
          <span class="px-2 py-1 bg-indigo-50 text-indigo-800 text-xs font-semibold rounded-full">
            Mission Control
          </span>
        </div>
        <div class="flex items-center gap-3">
          <button id="btnExport"
            class="bg-indigo-700 hover:bg-indigo-800 text-white px-4 py-2 rounded-lg text-sm font-semibold transition shadow-sm">
            Export JSON
          </button>
        </div>
      </div>
    </div>
  </nav>

  <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">

    <header class="mb-8 flex flex-col sm:flex-row sm:items-end justify-between gap-4">
      <div>
        <h1 class="text-3xl font-bold text-gray-900">Business Setup & Funding Status</h1>
        <p class="mt-2 text-gray-600">
          Live operational dashboard.
          <span id="asOf" class="ml-2 text-xs font-semibold px-2 py-1 rounded-full bg-gray-200 text-gray-800">As of: —</span>
          <span id="savedBadge" class="ml-2 text-xs font-semibold px-2 py-1 rounded-full bg-gray-100 text-gray-700">Saved: —</span>
        </p>
      </div>
    </header>

    <section class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-8">
      <div class="bg-white p-6 rounded-xl shadow-sm border-l-4 border-indigo-600">
        <p class="text-sm font-medium text-gray-500">Funding Target (Phase-1)</p>
        <p id="kpiTarget" class="text-2xl font-bold mt-1 text-gray-900">—</p>
      </div>

      <div class="bg-white p-6 rounded-xl shadow-sm border-l-4 border-emerald-600">
        <p class="text-sm font-medium text-gray-500">Capital Raised</p>
        <p id="kpiRaised" class="text-2xl font-bold mt-1 text-gray-900">—</p>
        <p id="kpiRaisedNote" class="text-xs mt-1 text-gray-500">—</p>
      </div>

      <div class="bg-white p-6 rounded-xl shadow-sm border-l-4 border-violet-600">
        <p class="text-sm font-medium text-gray-500">Runway (Est.)</p>
        <p id="kpiRunway" class="text-2xl font-bold mt-1 text-gray-900">—</p>
        <p id="kpiRunwayNote" class="text-xs mt-1 text-gray-500"></p>
      </div>

      <div class="bg-white p-6 rounded-xl shadow-sm border-l-4 border-gray-800">
        <p class="text-sm font-medium text-gray-500">Current Phase</p>
        <p id="kpiPhase" class="text-2xl font-bold mt-1 text-gray-900">—</p>
      </div>
    </section>

    <section class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-8">

      <div class="bg-white p-6 rounded-xl shadow-sm lg:col-span-1">
        <div class="flex items-center justify-between mb-4">
          <h2 class="text-lg font-bold">Reality Snapshot</h2>
          <span id="badgeConfirmed" class="text-xs font-semibold px-2 py-1 rounded-full bg-gray-100 text-gray-800">—</span>
        </div>
        
        <div class="space-y-4">
          <div class="p-3 bg-gray-50 rounded-lg border border-gray-100">
            <p class="text-xs font-medium text-gray-500 uppercase tracking-wide">Operations Status</p>
            <p id="opsStatus" class="text-base font-semibold text-gray-900 mt-1">—</p>
          </div>

          <div class="p-3 bg-gray-50 rounded-lg border border-gray-100">
            <p class="text-xs font-medium text-gray-500 uppercase tracking-wide">Assets Deployed</p>
            <ul id="assetsList" class="mt-2 space-y-1 text-sm text-gray-800 font-medium"></ul>
          </div>
          
          <div class="p-3 bg-gray-50 rounded-lg border border-gray-100">
             <p class="text-xs font-medium text-gray-500 uppercase tracking-wide">Next Milestones</p>
             <ol id="milestoneList" class="mt-2 space-y-2 text-sm text-gray-700 list-decimal list-inside"></ol>
          </div>
        </div>
      </div>

      <div class="bg-white p-6 rounded-xl shadow-sm lg:col-span-1 flex flex-col">
        <h2 class="text-lg font-bold mb-3">Funding Progress</h2>
        <p class="text-sm text-gray-600 mb-6">Gap to target based on current confirmed capital.</p>
        
        <div class="relative flex-grow flex items-center justify-center">
          <canvas id="fundingChart" style="max-height: 250px;"></canvas>
        </div>
      </div>

      <div class="bg-white p-6 rounded-xl shadow-sm lg:col-span-1 border border-indigo-100">
        <div class="flex items-center gap-2 mb-4">
            <svg class="w-5 h-5 text-indigo-600" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z"></path></svg>
            <h2 class="text-lg font-bold text-indigo-900">Revenue Scenario</h2>
        </div>
        <p class="text-sm text-gray-600 mb-4">Plan to hit $60k via operations (Bootstrapping).</p>
        
        <div class="space-y-4">
            <div>
                <label class="block text-xs font-medium text-gray-500 mb-1">Est. Day Rate ($)</label>
                <input type="number" id="calcRate" value="1200" class="w-full p-2 border border-gray-300 rounded text-sm font-mono">
            </div>
            <div>
                <label class="block text-xs font-medium text-gray-500 mb-1">Target Jobs / Month</label>
                <input type="number" id="calcJobs" value="4" class="w-full p-2 border border-gray-300 rounded text-sm font-mono">
            </div>
            
            <div class="pt-4 border-t border-gray-100">
                <div class="flex justify-between mb-2">
                    <span class="text-sm text-gray-600">Monthly Revenue:</span>
                    <span id="calcMonthly" class="text-sm font-bold text-emerald-600">$0</span>
                </div>
                <div class="flex justify-between">
                    <span class="text-sm text-gray-600">Time to $60k Goal:</span>
                    <span id="calcTime" class="text-sm font-bold text-indigo-600">0 Months</span>
                </div>
            </div>
        </div>
      </div>

    </section>

    <section class="bg-white p-6 rounded-xl shadow-sm">
      <h2 class="text-lg font-bold mb-2">System State (JSON)</h2>
      <p class="text-sm text-gray-600 mb-4">Update the JSON below to reflect reality. Click "Apply" to save.</p>

      <div class="grid grid-cols-1 lg:grid-cols-6 gap-4">
        <div class="lg:col-span-4">
          <textarea id="stateEditor"
            class="w-full h-48 font-mono text-xs p-3 border border-gray-300 rounded-lg bg-gray-50 text-slate-600"></textarea>
        </div>
        <div class="lg:col-span-2 flex flex-col gap-3 justify-start">
          <button id="btnApply"
            class="bg-gray-900 hover:bg-black text-white px-4 py-2 rounded-lg text-sm font-semibold shadow-md transition transform hover:-translate-y-0.5">
            Apply State (Save)
          </button>
          <button id="btnReset"
            class="bg-white hover:bg-gray-50 text-gray-900 border border-gray-300 px-4 py-2 rounded-lg text-sm font-semibold transition">
            Reset to Default
          </button>
          <div id="errBox"
            class="hidden p-3 rounded-lg border border-red-200 bg-red-50 text-red-800 text-sm"></div>
        </div>
      </div>
    </section>

  </main>

  <script>
    // =========================
    // 0) STORAGE KEY
    // =========================
    const STORAGE_KEY = "ifh_mission_control_state_v2";

    // =========================
    // 1) DEFAULT STATE (Truth from previous convo)
    // =========================
    const DEFAULT_STATE = {
      version: "v2",
      as_of: new Date().toISOString().slice(0, 10),
      phase: "Pre-Seed / Setup",
      funding_target: 60000,
      capital_raised: 0,
      capital_confirmed: false,
      runway_months: null,
      assets_owned: ["Nikon Z7"],
      operations_status: "Pre-revenue",
      next_milestones: [
        "Launch website",
        "Complete Part 107",
        "Acquire first drone",
        "Secure insurance"
      ]
    };

    // =========================
    // 2) HELPERS
    // =========================
    const fmtUSD = (n) => {
      if (typeof n !== "number" || !Number.isFinite(n)) return "—";
      return n.toLocaleString("en-US", { style: "currency", currency: "USD", maximumFractionDigits: 0 });
    };

    function normalizeState(raw) {
      const s = (raw && typeof raw === "object") ? raw : {};
      return {
        version: s.version || "v2",
        as_of: s.as_of || "",
        phase: s.phase || "—",
        funding_target: Number(s.funding_target) || 0,
        capital_raised: Number(s.capital_raised) || 0,
        capital_confirmed: s.capital_confirmed === true,
        runway_months: s.runway_months, // can be null
        assets_owned: Array.isArray(s.assets_owned) ? s.assets_owned : [],
        operations_status: s.operations_status || "—",
        next_milestones: Array.isArray(s.next_milestones) ? s.next_milestones : []
      };
    }

    function saveState(state) {
      const normalized = normalizeState(state);
      localStorage.setItem(STORAGE_KEY, JSON.stringify(normalized));
      setSavedBadge(true);
      return normalized;
    }

    function loadSavedState() {
      const raw = localStorage.getItem(STORAGE_KEY);
      if (!raw) return null;
      try { return normalizeState(JSON.parse(raw)); }
      catch { return null; }
    }

    function setSavedBadge(isSaved) {
      const b = document.getElementById("savedBadge");
      if (isSaved) {
        b.textContent = "Saved: YES";
        b.className = "ml-2 text-xs font-semibold px-2 py-1 rounded-full bg-emerald-100 text-emerald-800";
      } else {
        b.textContent = "Saved: NO";
        b.className = "ml-2 text-xs font-semibold px-2 py-1 rounded-full bg-gray-100 text-gray-700";
      }
    }

    // =========================
    // 3) RENDER LOGIC
    // =========================
    let fundingChartInstance = null;

    function render(state) {
      state = normalizeState(state);

      // Simple Text Updates
      document.getElementById("asOf").textContent = state.as_of ? `As of: ${state.as_of}` : "As of: —";
      document.getElementById("kpiTarget").textContent = fmtUSD(state.funding_target);
      document.getElementById("kpiRaised").textContent = fmtUSD(state.capital_raised);
      document.getElementById("kpiPhase").textContent = state.phase;
      document.getElementById("opsStatus").textContent = state.operations_status;
      
      // Logic: Raised Note
      const raisedNote = document.getElementById("kpiRaisedNote");
      if (!state.capital_confirmed && state.capital_raised === 0) {
        raisedNote.textContent = "Capital pending confirmation";
        raisedNote.className = "text-xs mt-1 text-gray-400";
      } else if (state.capital_confirmed) {
        const pct = Math.round((state.capital_raised / state.funding_target) * 100);
        raisedNote.textContent = `${pct}% of Goal`;
        raisedNote.className = "text-xs mt-1 text-emerald-600 font-bold";
      }

      // Logic: Runway
      const runwayEl = document.getElementById("kpiRunway");
      const runwayNoteEl = document.getElementById("kpiRunwayNote");
      if (state.runway_months !== null && state.runway_months !== undefined) {
         runwayEl.textContent = state.runway_months;
         runwayNoteEl.textContent = "Months remaining";
      } else {
         runwayEl.textContent = "—";
         runwayNoteEl.textContent = "Pending funding";
      }

      // Logic: Confirmed Badge
      const badge = document.getElementById("badgeConfirmed");
      if (state.capital_confirmed) {
        badge.textContent = "Confirmed";
        badge.className = "text-xs font-semibold px-2 py-1 rounded-full bg-emerald-100 text-emerald-800 border border-emerald-200";
      } else {
        badge.textContent = "Unconfirmed";
        badge.className = "text-xs font-semibold px-2 py-1 rounded-full bg-amber-100 text-amber-800 border border-amber-200";
      }

      // Lists
      const assetsList = document.getElementById("assetsList");
      assetsList.innerHTML = state.assets_owned.map(a => `<li>• ${a}</li>`).join("");
      
      const milestoneList = document.getElementById("milestoneList");
      milestoneList.innerHTML = state.next_milestones.map(m => `<li>${m}</li>`).join("");

      // Chart
      renderChart(state);
    }

    function renderChart(state) {
      const ctx = document.getElementById("fundingChart").getContext("2d");
      const remaining = Math.max(0, state.funding_target - state.capital_raised);
      
      const data = {
        labels: ["Raised", "Needed"],
        datasets: [{
          data: [state.capital_raised, remaining],
          backgroundColor: ["#10b981", "#e5e7eb"],
          borderWidth: 0,
          hoverOffset: 4
        }]
      };

      if (fundingChartInstance) {
        fundingChartInstance.data = data;
        fundingChartInstance.update();
      } else {
        fundingChartInstance = new Chart(ctx, {
          type: "doughnut",
          data: data,
          options: {
            responsive: true,
            maintainAspectRatio: false,
            cutout: '70%',
            plugins: {
              legend: { position: 'bottom', labels: { usePointStyle: true, boxWidth: 8 } }
            }
          }
        });
      }
    }

    // =========================
    // 4) REVENUE CALCULATOR
    // =========================
    function updateCalculator(targetAmount) {
        const rate = parseFloat(document.getElementById("calcRate").value) || 0;
        const jobs = parseFloat(document.getElementById("calcJobs").value) || 0;
        
        const monthly = rate * jobs;
        document.getElementById("calcMonthly").textContent = fmtUSD(monthly);
        
        const timeEl = document.getElementById("calcTime");
        if (monthly > 0) {
            const months = (targetAmount / monthly).toFixed(1);
            timeEl.textContent = `${months} Months`;
        } else {
            timeEl.textContent = "∞";
        }
    }

    // =========================
    // 5) INITIALIZATION & LISTENERS
    // =========================
    const editor = document.getElementById("stateEditor");
    const errBox = document.getElementById("errBox");

    // Load initial state
    let currentState = loadSavedState() || normalizeState(DEFAULT_STATE);
    editor.value = JSON.stringify(currentState, null, 2);
    render(currentState);
    updateCalculator(currentState.funding_target); // Init calc

    // Apply Button
    document.getElementById("btnApply").addEventListener("click", () => {
      try {
        const parsed = JSON.parse(editor.value);
        currentState = saveState(parsed); // Save & Normalize
        editor.value = JSON.stringify(currentState, null, 2); // Reformat
        render(currentState);
        updateCalculator(currentState.funding_target); // Update calc goal
        errBox.classList.add("hidden");
      } catch (e) {
        errBox.textContent = "JSON Error: " + e.message;
        errBox.classList.remove("hidden");
      }
    });

    // Reset Button
    document.getElementById("btnReset").addEventListener("click", () => {
      localStorage.removeItem(STORAGE_KEY);
      setSavedBadge(false);
      currentState = normalizeState(DEFAULT_STATE);
      editor.value = JSON.stringify(currentState, null, 2);
      render(currentState);
      updateCalculator(currentState.funding_target);
    });

    // Calculator Listeners
    ['calcRate', 'calcJobs'].forEach(id => {
        document.getElementById(id).addEventListener('input', () => {
            updateCalculator(currentState.funding_target);
        });
    });

    // Export Button
    document.getElementById("btnExport").addEventListener("click", () => {
        const blob = new Blob([editor.value], {type: "application/json"});
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = `IFH_MissionControl_${new Date().toISOString().slice(0,10)}.json`;
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
    });

  </script>
</body>
</html>
