/* app.js - Analog Modulation Simulator */
// Global State
const state = {
  Am: 5.0,        // Message Amplitude (V)
  fm: 100,        // Message Frequency (Hz)
  Ac: 5.0,        // Carrier Amplitude (V)
  fc: 1000,       // Carrier Frequency (Hz)
  m: 1.0,         // Modulation Index (Am / Ac)
  
  // Animation settings
  isPlaying: false,
  timeOffset: 0,
  lastTime: 0,
  
  // View settings
  showEnvelope: true,
  theme: 'dark' // 'dark' or 'light'
};
// Chart instances
let messageChart = null;
let carrierChart = null;
let amChart = null;
// DOM Elements
const elements = {
  // Inputs
  amSlider: document.getElementById('amSlider'),
  amVal: document.getElementById('amVal'),
  fmSlider: document.getElementById('fmSlider'),
  fmVal: document.getElementById('fmVal'),
  acSlider: document.getElementById('acSlider'),
  acVal: document.getElementById('acVal'),
  fcSlider: document.getElementById('fcSlider'),
  fcVal: document.getElementById('fcVal'),
  mSlider: document.getElementById('mSlider'),
  mVal: document.getElementById('mVal'),
  
  // Buttons & Controls
  playBtn: document.getElementById('playBtn'),
  playBtnText: document.getElementById('playBtnText'),
  resetBtn: document.getElementById('resetBtn'),
  resetZoomBtn: document.getElementById('resetZoomBtn'),
  themeToggle: document.getElementById('themeToggle'),
  sunIcon: document.getElementById('sunIcon'),
  moonIcon: document.getElementById('moonIcon'),
  envelopeCheckbox: document.getElementById('envelopeCheckbox'),
  
  // Panels & Outputs
  warningPanel: document.getElementById('warningPanel'),
  mMetric: document.getElementById('mMetric'),
  powerMetric: document.getElementById('powerMetric'),
  vMaxMetric: document.getElementById('vMaxMetric'),
  vMinMetric: document.getElementById('vMinMetric'),
  
  // Tabs
  tabButtons: document.querySelectorAll('.tab-btn'),
  tabContents: document.querySelectorAll('.tab-content')
};
// Default Values (for reset)
const DEFAULTS = {
  Am: 5.0,
  fm: 100,
  Ac: 5.0,
  fc: 1000,
  m: 1.0
};
// -------------------------------------------------------------
// 1. Initial Setup and Theme Management
// -------------------------------------------------------------
document.addEventListener('DOMContentLoaded', () => {
  // Initialize KaTeX equation rendering
  if (typeof renderMathInElement === 'function') {
    renderMathInElement(document.body, {
      delimiters: [
        { left: '$$', right: '$$', display: true },
        { left: '$', right: '$', display: false }
      ]
    });
  }
  // Setup Event Listeners
  initEventListeners();
  
  // Set default theme from user preference or HTML default (dark)
  const isLight = document.body.classList.contains('light-mode');
  state.theme = isLight ? 'light' : 'dark';
  updateThemeIcons();
  // Initialize and Render Charts
  initCharts();
  
  // Initial draw
  updateSimulation();
});
// Sync Theme Icons
function updateThemeIcons() {
  if (state.theme === 'light') {
    elements.sunIcon.style.display = 'none';
    elements.moonIcon.style.display = 'block';
  } else {
    elements.sunIcon.style.display = 'block';
    elements.moonIcon.style.display = 'none';
  }
}
// Toggle Dark/Light Mode
function toggleTheme() {
  if (state.theme === 'dark') {
    document.body.classList.add('light-mode');
    state.theme = 'light';
  } else {
    document.body.classList.remove('light-mode');
    state.theme = 'dark';
  }
  updateThemeIcons();
  
  // Re-initialize charts with the new theme colors
  updateChartThemes();
}
// Get Colors dynamically based on the CSS variables
function getThemeColors() {
  const style = getComputedStyle(document.body);
  return {
    text: style.getPropertyValue('--text-primary').trim(),
    secondaryText: style.getPropertyValue('--text-secondary').trim(),
    border: style.getPropertyValue('--bg-card-border').trim(),
    
    // Waveform colors
    message: style.getPropertyValue('--color-message').trim(),
    carrier: style.getPropertyValue('--color-carrier').trim(),
    am: style.getPropertyValue('--color-am').trim(),
    envelope: style.getPropertyValue('--color-envelope').trim()
  };
}
// -------------------------------------------------------------
// 2. Event Listeners Setup
// -------------------------------------------------------------
function initEventListeners() {
  // Theme Toggle Button
  elements.themeToggle.addEventListener('click', toggleTheme);
  // Link sliders and numerical values
  linkInputControls('am', (val) => {
    state.Am = val;
    // Calculate new m: m = Am / Ac
    state.m = state.Am / state.Ac;
    updateControlValues(['m']);
  });
  linkInputControls('fm', (val) => {
    state.fm = val;
  });
  linkInputControls('ac', (val) => {
    state.Ac = val;
    // Calculate new m: m = Am / Ac
    state.m = state.Am / state.Ac;
    updateControlValues(['m']);
  });
  linkInputControls('fc', (val) => {
    state.fc = val;
  });
  linkInputControls('m', (val) => {
    state.m = val;
    // Calculate new Am: Am = m * Ac
    const calculatedAm = state.m * state.Ac;
    // Clamp to slider bounds
    state.Am = Math.min(10.0, Math.max(0.0, calculatedAm));
    // If clamped, recalculate modulation index to represent exact state
    if (calculatedAm > 10.0) {
      state.m = state.Am / state.Ac;
    }
    updateControlValues(['am', 'm']);
  });
  // Play / Pause Sweep
  elements.playBtn.addEventListener('click', togglePlay);
  // Reset Button
  elements.resetBtn.addEventListener('click', resetSimulation);
  // Reset Zoom
  elements.resetZoomBtn.addEventListener('click', resetChartsZoom);
  // Envelope Checkbox
  elements.envelopeCheckbox.addEventListener('change', (e) => {
    state.showEnvelope = e.target.checked;
    updateSimulation();
  });
  // Educational Tabs logic
  elements.tabButtons.forEach(btn => {
    btn.addEventListener('click', () => {
      // Remove active from all tabs
      elements.tabButtons.forEach(b => b.classList.remove('active'));
      elements.tabContents.forEach(c => c.classList.remove('active'));
      // Add active to current
      btn.classList.add('active');
      const tabId = btn.getAttribute('data-tab') + 'Tab';
      document.getElementById(tabId).classList.add('active');
    });
  });
}
// Helper to bind slider & numerical inputs together
function linkInputControls(paramName, updateCallback) {
  const slider = elements[`${paramName}Slider`];
  const input = elements[`${paramName}Val`];
  // Slider change
  slider.addEventListener('input', (e) => {
    const val = parseFloat(e.target.value);
    input.value = val;
    updateCallback(val);
    updateSimulation();
  });
  // Number input change
  input.addEventListener('change', (e) => {
    let val = parseFloat(e.target.value);
    const min = parseFloat(input.getAttribute('min'));
    const max = parseFloat(input.getAttribute('max'));
    
    // Validate value bounds
    if (isNaN(val)) val = DEFAULTS[paramName.charAt(0).toUpperCase() + paramName.slice(1)];
    if (val < min) val = min;
    if (val > max) val = max;
    
    input.value = val.toFixed(1);
    slider.value = val;
    updateCallback(val);
    updateSimulation();
  });
}
// Helper to update control inputs when recalculations happen
function updateControlValues(paramList) {
  paramList.forEach(param => {
    const slider = elements[`${param}Slider`];
    const input = elements[`${param}Val`];
    const val = state[param === 'm' ? 'm' : param.charAt(0).toUpperCase() + param.slice(1)];
    
    slider.value = val;
    input.value = val.toFixed(param === 'm' ? 2 : 1);
  });
}
// -------------------------------------------------------------
// 3. Mathematical Waveform Generation
// -------------------------------------------------------------
function generateWaveformData() {
  const N = 1000; // Sample points
  
  // Show exactly 2 cycles of the message wave to make the envelope shape consistently visible.
  const T = 2 / state.fm; 
  const dt = T / N;
  
  const timeLabels = [];
  const messageData = [];
  const carrierData = [];
  const amData = [];
  const envelopeUpper = [];
  const envelopeLower = [];
  for (let i = 0; i <= N; i++) {
    const t = i * dt + state.timeOffset;
    const tLabel = i * dt; // Display static time on the X-axis starting from 0
    timeLabels.push(tLabel.toFixed(6));
    
    // 1. Message Signal: m(t) = Am * cos(2 * pi * fm * t)
    const m_t = state.Am * Math.cos(2 * Math.PI * state.fm * t);
    messageData.push(m_t);
    
    // 2. Carrier Signal: c(t) = Ac * cos(2 * pi * fc * t)
    const c_t = state.Ac * Math.cos(2 * Math.PI * state.fc * t);
    carrierData.push(c_t);
    
    // 3. Modulated AM Signal: s(t) = Ac * (1 + m * cos(2*pi*fm*t)) * cos(2*pi*fc*t)
    const s_t = state.Ac * (1 + state.m * Math.cos(2 * Math.PI * state.fm * t)) * Math.cos(2 * Math.PI * state.fc * t);
    amData.push(s_t);
    // Envelopes: Ac * (1 +/- m * cos(2*pi*fm*t))
    const env_t = state.Ac * (1 + state.m * Math.cos(2 * Math.PI * state.fm * t));
    envelopeUpper.push(env_t);
    envelopeLower.push(-env_t);
  }
  return {
    labels: timeLabels,
    message: messageData,
    carrier: carrierData,
    am: amData,
    envUpper: envelopeUpper,
    envLower: envelopeLower
  };
}
// -------------------------------------------------------------
// 4. Chart.js Setup
// -------------------------------------------------------------
function initCharts() {
  const colors = getThemeColors();
  const fontConfig = {
    family: 'Inter',
    size: 11
  };
  
  const commonOptions = (titleText, gridColor, textColor, yMin, yMax) => ({
    responsive: true,
    maintainAspectRatio: false,
    animation: false, // Turn off animation for real-time redraw speed
    plugins: {
      legend: {
        display: true,
        position: 'top',
        align: 'end',
        labels: {
          color: textColor,
          font: fontConfig,
          boxWidth: 12,
          padding: 8
        }
      },
      zoom: {
        pan: {
          enabled: true,
          mode: 'x',
        },
        zoom: {
          wheel: {
            enabled: true,
          },
          drag: {
            enabled: true,
            backgroundColor: 'rgba(99, 102, 241, 0.1)',
            borderColor: 'rgba(99, 102, 241, 0.4)'
          },
          mode: 'x',
        }
      }
    },
    scales: {
      x: {
        grid: {
          color: gridColor,
          borderColor: gridColor
        },
        ticks: {
          color: textColor,
          font: fontConfig,
          maxTicksLimit: 10,
          callback: function(value) {
            // Convert to ms for readable label
            return (parseFloat(this.getLabelForValue(value)) * 1000).toFixed(1) + ' ms';
          }
        },
        title: {
          display: true,
          text: 'Time (ms)',
          color: textColor,
          font: fontConfig
        }
      },
      y: {
        min: yMin,
        max: yMax,
        grid: {
          color: gridColor,
          borderColor: gridColor
        },
        ticks: {
          color: textColor,
          font: fontConfig
        },
        title: {
          display: true,
          text: 'Amplitude (V)',
          color: textColor,
          font: fontConfig
        }
      }
    }
  });
  const gridColor = state.theme === 'dark' ? 'rgba(255, 255, 255, 0.05)' : 'rgba(15, 23, 42, 0.05)';
  const textColor = colors.secondaryText;
  // 1. Message Chart
  const ctxM = document.getElementById('messageChart').getContext('2d');
  messageChart = new Chart(ctxM, {
    type: 'line',
    data: {
      labels: [],
      datasets: [{
        label: 'Message Signal m(t)',
        data: [],
        borderColor: colors.message,
        borderWidth: 2,
        pointRadius: 0,
        fill: false
      }]
    },
    options: commonOptions('Message Signal', gridColor, textColor, -11, 11)
  });
  // 2. Carrier Chart
  const ctxC = document.getElementById('carrierChart').getContext('2d');
  carrierChart = new Chart(ctxC, {
    type: 'line',
    data: {
      labels: [],
      datasets: [{
        label: 'Carrier Signal c(t)',
        data: [],
        borderColor: colors.carrier,
        borderWidth: 1.5,
        pointRadius: 0,
        fill: false
      }]
    },
    options: commonOptions('Carrier Signal', gridColor, textColor, -11, 11)
  });
  // 3. AM Chart
  const ctxAm = document.getElementById('amChart').getContext('2d');
  amChart = new Chart(ctxAm, {
    type: 'line',
    data: {
      labels: [],
      datasets: [
        {
          label: 'Modulated AM Signal s(t)',
          data: [],
          borderColor: colors.am,
          borderWidth: 1.5,
          pointRadius: 0,
          fill: false,
          order: 2
        },
        {
          label: 'Upper Envelope',
          data: [],
          borderColor: colors.envelope,
          borderWidth: 1.5,
          borderDash: [5, 5],
          pointRadius: 0,
          fill: false,
          hidden: false,
          order: 1
        },
        {
          label: 'Lower Envelope',
          data: [],
          borderColor: colors.envelope,
          borderWidth: 1.5,
          borderDash: [5, 5],
          pointRadius: 0,
          fill: false,
          hidden: false,
          order: 1
        }
      ]
    },
    options: commonOptions('Amplitude Modulated Signal', gridColor, textColor, -21, 21)
  });
}
// Update Chart styling when switching themes
function updateChartThemes() {
  const colors = getThemeColors();
  const gridColor = state.theme === 'dark' ? 'rgba(255, 255, 255, 0.05)' : 'rgba(15, 23, 42, 0.05)';
  const textColor = colors.secondaryText;
  
  [messageChart, carrierChart, amChart].forEach(chart => {
    chart.options.scales.x.grid.color = gridColor;
    chart.options.scales.x.ticks.color = textColor;
    chart.options.scales.x.title.color = textColor;
    
    chart.options.scales.y.grid.color = gridColor;
    chart.options.scales.y.ticks.color = textColor;
    chart.options.scales.y.title.color = textColor;
    
    chart.options.plugins.legend.labels.color = textColor;
  });
  // Update line colors
  messageChart.data.datasets[0].borderColor = colors.message;
  carrierChart.data.datasets[0].borderColor = colors.carrier;
  amChart.data.datasets[0].borderColor = colors.am;
  amChart.data.datasets[1].borderColor = colors.envelope;
  amChart.data.datasets[2].borderColor = colors.envelope;
  updateSimulation();
}
// Reset Zoom Function
function resetChartsZoom() {
  if (messageChart && carrierChart && amChart) {
    messageChart.resetZoom();
    carrierChart.resetZoom();
    amChart.resetZoom();
  }
}
// -------------------------------------------------------------
// 5. Simulation & UI Updates
// -------------------------------------------------------------
function updateSimulation() {
  const data = generateWaveformData();
  
  // 1. Update Message Chart
  messageChart.data.labels = data.labels;
  messageChart.data.datasets[0].data = data.message;
  messageChart.update('none'); // Update without canvas-refresh animations
  // 2. Update Carrier Chart
  carrierChart.data.labels = data.labels;
  carrierChart.data.datasets[0].data = data.carrier;
  carrierChart.update('none');
  // 3. Update AM Chart
  amChart.data.labels = data.labels;
  amChart.data.datasets[0].data = data.am;
  
  // Toggle Envelope lines visibility
  amChart.data.datasets[1].data = data.envUpper;
  amChart.data.datasets[2].data = data.envLower;
  amChart.setDatasetVisibility(1, state.showEnvelope);
  amChart.setDatasetVisibility(2, state.showEnvelope);
  
  // Dynamic scale adjustment for AM chart based on peak AM voltage to prevent clipping
  const maxVoltage = state.Ac * (1 + state.m);
  const scaleLimit = Math.ceil(maxVoltage + 2); // padding of 2V
  amChart.options.scales.y.min = -scaleLimit;
  amChart.options.scales.y.max = scaleLimit;
  
  amChart.update('none');
  // 4. Update Metrics Display
  updateMetricsDisplay();
}
function updateMetricsDisplay() {
  // Calculated Modulation Index
  elements.mMetric.textContent = state.m.toFixed(2);
  if (state.m > 1) {
    elements.mMetric.classList.add('warn');
    elements.warningPanel.classList.add('visible');
  } else {
    elements.mMetric.classList.remove('warn');
    elements.warningPanel.classList.remove('visible');
  }
  // Sideband Power Ratio
  // P_sb / P_total = m^2 / (2 + m^2)
  const powerRatio = (state.m * state.m) / (2 + (state.m * state.m));
  elements.powerMetric.textContent = (powerRatio * 100).toFixed(1) + '%';
  // Peak and Envelope limits
  const vMax = state.Ac * (1 + state.m);
  const vMin = state.Ac * (1 - state.m);
  
  elements.vMaxMetric.textContent = vMax.toFixed(1) + ' V';
  elements.vMinMetric.textContent = vMin.toFixed(1) + ' V';
  
  if (state.m > 1) {
    elements.vMinMetric.classList.add('warn');
  } else {
    elements.vMinMetric.classList.remove('warn');
  }
}
// -------------------------------------------------------------
// 6. Animation Sweep Logic (Oscilloscope sweep)
// -------------------------------------------------------------
function togglePlay() {
  state.isPlaying = !state.isPlaying;
  
  if (state.isPlaying) {
    elements.playBtn.classList.add('animating');
    elements.playBtnText.textContent = 'Pause sweep';
    document.querySelector('.play-icon').style.display = 'none';
    document.querySelector('.pause-icon').style.display = 'block';
    
    state.lastTime = performance.now();
    requestAnimationFrame(animationLoop);
  } else {
    elements.playBtn.classList.remove('animating');
    elements.playBtnText.textContent = 'Run sweep';
    document.querySelector('.play-icon').style.display = 'block';
    document.querySelector('.pause-icon').style.display = 'none';
  }
}
function animationLoop(timestamp) {
  if (!state.isPlaying) return;
  const delta = timestamp - state.lastTime;
  state.lastTime = timestamp;
  // Let the sweep speed be proportional to the message frequency, 
  // ensuring the animation movement is visible and elegant
  // At fm = 100Hz, we shift the window by 0.001 seconds per second.
  // Increment speed relative to actual milliseconds passed
  const speedScale = 0.05 / state.fm; // sweep movement normalized to signal cycles
  state.timeOffset += (delta / 1000) * speedScale;
  // Keep offset small to prevent floating point inaccuracy over long periods
  const T = 1 / state.fm;
  if (state.timeOffset > T) {
    state.timeOffset = state.timeOffset % T;
  }
  updateSimulation();
  
  requestAnimationFrame(animationLoop);
}
// Reset Simulation back to defaults
function resetSimulation() {
  // Stop animation if running
  if (state.isPlaying) {
    togglePlay();
  }
  // Restore states
  state.Am = DEFAULTS.Am;
  state.fm = DEFAULTS.fm;
  state.Ac = DEFAULTS.Ac;
  state.fc = DEFAULTS.fc;
  state.m = DEFAULTS.m;
  state.timeOffset = 0;
  // Update UI control positions
  updateControlValues(['am', 'fm', 'ac', 'fc', 'm']);
  // Reset charts zoom levels
  resetChartsZoom();
  // Run update
  updateSimulation();
}
