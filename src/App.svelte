<script>
  import PomodoroTimer from './components/PomodoroTimer.svelte'
  import SunsetOverlay from './components/SunsetOverlay.svelte'
  import SessionStats from './components/SessionStats.svelte'
  import SettingsPanel from './components/SettingsPanel.svelte'

  let workDuration = 50
  let breakDuration = 10
  let sessionsCompleted = 0
  let showSettings = false
  let sunsetProgress = 0
  let isWorkSession = true

  function handleSessionComplete() {
    sessionsCompleted++
  }

  function handleSunsetProgress(event) {
    sunsetProgress = event.detail
  }

  function handleSessionChange(event) {
    isWorkSession = event.detail
  }

  function handleSettingsChange(event) {
    workDuration = event.detail.workDuration
    breakDuration = event.detail.breakDuration
    showSettings = false
  }
</script>

<div class="app-container">
  <SunsetOverlay progress={sunsetProgress} isWorkSession={isWorkSession} />

  <header class="app-header">
    <h1>🍅 Pomodoro Screen</h1>
    <p class="subtitle">Concentración con el atardecer</p>
  </header>

  <main class="app-main">
    <PomodoroTimer
      {workDuration}
      {breakDuration}
      on:sessionComplete={handleSessionComplete}
      on:sunsetProgress={handleSunsetProgress}
      on:sessionChange={handleSessionChange}
    />

    <SessionStats {sessionsCompleted} />

    {#if showSettings}
      <SettingsPanel
        {workDuration}
        {breakDuration}
        on:save={handleSettingsChange}
        on:cancel={() => (showSettings = false)}
      />
    {/if}

    <button
      class="settings-btn"
      on:click={() => (showSettings = !showSettings)}
      title="Configuración"
    >
      ⚙️ Configuración
    </button>
  </main>

  <footer class="app-footer">
    <p>Hecho con ❤️ para tu concentración</p>
  </footer>
</div>

<style global>
  :root {
    --color-primary: #ff6b6b;
    --color-secondary: #4ecdc4;
    --color-dark: #2c3e50;
    --color-light: #ecf0f1;
    --color-gray: #95a5a6;
    --transition: all 0.3s ease;
  }

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: var(--color-dark);
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
  }

  html,
  body,
  #app {
    width: 100%;
    height: 100%;
  }
</style>

<style>
  .app-container {
    background: white;
    border-radius: 20px;
    box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
    max-width: 600px;
    width: 100%;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    position: relative;
  }

  .app-header {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 40px 30px;
    text-align: center;
    position: relative;
    z-index: 10;
  }

  .app-header h1 {
    font-size: 2.5rem;
    margin-bottom: 10px;
    font-weight: 700;
  }

  .subtitle {
    font-size: 1rem;
    opacity: 0.9;
    font-weight: 300;
  }

  .app-main {
    flex: 1;
    padding: 40px 30px;
    position: relative;
    z-index: 10;
  }

  .settings-btn {
    position: absolute;
    top: 20px;
    right: 20px;
    background: var(--color-light);
    border: 2px solid var(--color-gray);
    padding: 10px 20px;
    border-radius: 50px;
    cursor: pointer;
    font-size: 0.9rem;
    font-weight: 600;
    transition: var(--transition);
    z-index: 20;
  }

  .settings-btn:hover {
    background: var(--color-primary);
    color: white;
    border-color: var(--color-primary);
    transform: scale(1.05);
  }

  .app-footer {
    background: #f8f9fa;
    padding: 20px;
    text-align: center;
    color: var(--color-gray);
    font-size: 0.9rem;
    border-top: 1px solid #e0e0e0;
    position: relative;
    z-index: 10;
  }

  @media (max-width: 480px) {
    .app-header h1 {
      font-size: 2rem;
    }

    .app-header {
      padding: 30px 20px;
    }

    .app-main {
      padding: 30px 20px;
    }
  }
</style>
