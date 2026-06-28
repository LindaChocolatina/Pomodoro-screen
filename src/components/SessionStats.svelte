<script>
  export let sessionsCompleted = 0

  const totalTimeWorked = sessionsCompleted * 50 // 50 minutos por sesión
  const totalTimeBreak = sessionsCompleted * 10 // 10 minutos de descanso
</script>

<div class="stats-container">
  <h2>📊 Estadísticas de Hoy</h2>
  <div class="stats-grid">
    <div class="stat-card">
      <div class="stat-icon">🏃</div>
      <div class="stat-content">
        <p class="stat-label">Sesiones Completadas</p>
        <p class="stat-value">{sessionsCompleted}</p>
      </div>
    </div>

    <div class="stat-card">
      <div class="stat-icon">⏱️</div>
      <div class="stat-content">
        <p class="stat-label">Tiempo de Trabajo</p>
        <p class="stat-value">{totalTimeWorked} min</p>
      </div>
    </div>

    <div class="stat-card">
      <div class="stat-icon">☕</div>
      <div class="stat-content">
        <p class="stat-label">Tiempo de Descanso</p>
        <p class="stat-value">{totalTimeBreak} min</p>
      </div>
    </div>
  </div>
</div>

<style>
  .stats-container {
    margin-top: 40px;
    padding-top: 30px;
    border-top: 2px solid #e0e0e0;
  }

  .stats-container h2 {
    text-align: center;
    color: #2c3e50;
    margin-bottom: 25px;
    font-size: 1.5rem;
  }

  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 20px;
  }

  .stat-card {
    background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
    border-radius: 15px;
    padding: 20px;
    display: flex;
    align-items: center;
    gap: 15px;
    transition: all 0.3s ease;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
  }

  .stat-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
  }

  .stat-icon {
    font-size: 2rem;
  }

  .stat-content {
    flex: 1;
  }

  .stat-label {
    font-size: 0.85rem;
    color: #95a5a6;
    margin-bottom: 5px;
    font-weight: 500;
  }

  .stat-value {
    font-size: 1.8rem;
    font-weight: 700;
    color: #2c3e50;
    font-variant-numeric: tabular-nums;
  }

  @media (max-width: 480px) {
    .stats-grid {
      grid-template-columns: 1fr;
    }

    .stat-value {
      font-size: 1.5rem;
    }
  }
</style>
