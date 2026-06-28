<script>
  import { createEventDispatcher, onMount } from 'svelte'

  export let workDuration = 50
  export let breakDuration = 10

  const dispatch = createEventDispatcher()

  let timeLeft = workDuration * 60
  let isRunning = false
  let isWorkSession = true
  let sessionsInCycle = 0
  let intervalId = null

  const totalTime = isWorkSession ? workDuration * 60 : breakDuration * 60
  $: progress = ((totalTime - timeLeft) / totalTime) * 100

  onMount(() => {
    return () => {
      if (intervalId) clearInterval(intervalId)
    }
  })

  function updateTimer() {
    if (isRunning) {
      intervalId = setInterval(() => {
        timeLeft--
        const currentTotal = isWorkSession ? workDuration * 60 : breakDuration * 60
        const currentProgress = ((currentTotal - timeLeft) / currentTotal) * 100
        dispatch('sunsetProgress', currentProgress)

        if (timeLeft <= 0) {
          handleSessionEnd()
        }
      }, 1000)
    } else if (intervalId) {
      clearInterval(intervalId)
    }
  }

  function handleSessionEnd() {
    clearInterval(intervalId)
    isRunning = false

    if (isWorkSession) {
      sessionsInCycle++
      dispatch('sessionComplete')
      isWorkSession = false
      dispatch('sessionChange', false)
      timeLeft = breakDuration * 60
    } else {
      isWorkSession = true
      dispatch('sessionChange', true)
      timeLeft = workDuration * 60
    }
  }

  function toggleTimer() {
    isRunning = !isRunning
    updateTimer()
  }

  function skipSession() {
    clearInterval(intervalId)
    isRunning = false
    handleSessionEnd()
  }

  function resetTimer() {
    clearInterval(intervalId)
    isRunning = false
    isWorkSession = true
    dispatch('sessionChange', true)
    timeLeft = workDuration * 60
    sessionsInCycle = 0
    dispatch('sunsetProgress', 0)
  }

  $: if (workDuration && !isRunning && isWorkSession) {
    timeLeft = workDuration * 60
  }

  const minutes = Math.floor(timeLeft / 60)
  const seconds = timeLeft % 60
  const displayTime = `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`
</script>

<div class="timer-container">
  <div class="session-indicator">
    <span class="badge" class:work={isWorkSession} class:break={!isWorkSession}>
      {isWorkSession ? '🏃 Trabajo' : '☕ Descanso'}
    </span>
    <span class="sessions-count">Sesión {sessionsInCycle + 1}</span>
  </div>

  <div class="timer-display">
    <div class="progress-ring-container">
      <svg class="progress-ring" viewBox="0 0 200 200">
        <circle cx="100" cy="100" r="90" fill="none" stroke="#e0e0e0" stroke-width="8" />
        <circle
          cx="100"
          cy="100"
          r="90"
          fill="none"
          stroke={isWorkSession ? '#ff6b6b' : '#4ecdc4'}
          stroke-width="8"
          stroke-dasharray={`${(565 * progress) / 100} 565`}
          stroke-linecap="round"
          transform="rotate(-90 100 100)"
          class="progress-circle"
        />
      </svg>
      <div class="time-display">{displayTime}</div>
    </div>
  </div>

  <div class="timer-controls">
    <button class="control-btn play-btn" on:click={toggleTimer} title={isRunning ? 'Pausar' : 'Iniciar'}>
      {isRunning ? '⏸️ Pausar' : '▶️ Iniciar'}
    </button>
    <button class="control-btn skip-btn" on:click={skipSession} title="Saltar sesión">
      ⏭️ Saltar
    </button>
    <button class="control-btn reset-btn" on:click={resetTimer} title="Reiniciar">
      🔄 Reiniciar
    </button>
  </div>

  <div class="timer-info">
    <p>Trabajo: {workDuration} min | Descanso: {breakDuration} min</p>
  </div>
</div>

<style>
  .timer-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 30px;
  }

  .session-indicator {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
    width: 100%;
    flex-wrap: wrap;
  }

  .badge {
    display: inline-block;
    padding: 8px 16px;
    border-radius: 50px;
    font-weight: 600;
    font-size: 0.9rem;
  }

  .badge.work {
    background: #ffe0e0;
    color: #ff6b6b;
  }

  .badge.break {
    background: #e0f7f5;
    color: #4ecdc4;
  }

  .sessions-count {
    font-size: 0.9rem;
    color: #95a5a6;
    font-weight: 500;
  }

  .timer-display {
    width: 100%;
    display: flex;
    justify-content: center;
  }

  .progress-ring-container {
    position: relative;
    width: 250px;
    height: 250px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .progress-ring {
    width: 100%;
    height: 100%;
    transform: rotateY(180deg) rotateZ(180deg);
  }

  .progress-circle {
    transition: stroke-dasharray 1s linear;
  }

  .time-display {
    position: absolute;
    font-size: 3.5rem;
    font-weight: 700;
    color: #2c3e50;
    font-variant-numeric: tabular-nums;
  }

  .timer-controls {
    display: flex;
    gap: 15px;
    justify-content: center;
    flex-wrap: wrap;
    width: 100%;
  }

  .control-btn {
    padding: 12px 24px;
    border: none;
    border-radius: 50px;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    min-width: 120px;
  }

  .play-btn {
    background: #ff6b6b;
    color: white;
  }

  .play-btn:hover {
    background: #ff5252;
    transform: translateY(-2px);
    box-shadow: 0 10px 20px rgba(255, 107, 107, 0.3);
  }

  .skip-btn {
    background: #4ecdc4;
    color: white;
  }

  .skip-btn:hover {
    background: #45b7ae;
    transform: translateY(-2px);
    box-shadow: 0 10px 20px rgba(78, 205, 196, 0.3);
  }

  .reset-btn {
    background: #ecf0f1;
    color: #2c3e50;
    border: 2px solid #95a5a6;
  }

  .reset-btn:hover {
    background: #d5d8dc;
    transform: translateY(-2px);
  }

  .timer-info {
    text-align: center;
    color: #95a5a6;
    font-size: 0.9rem;
  }

  @media (max-width: 480px) {
    .progress-ring-container {
      width: 200px;
      height: 200px;
    }

    .time-display {
      font-size: 2.5rem;
    }

    .control-btn {
      padding: 10px 20px;
      font-size: 0.9rem;
      min-width: 100px;
    }
  }
</style>
