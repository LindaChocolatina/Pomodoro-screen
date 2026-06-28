<script>
  import { createEventDispatcher } from 'svelte'

  export let workDuration = 50
  export let breakDuration = 10

  const dispatch = createEventDispatcher()

  let newWorkDuration = workDuration
  let newBreakDuration = breakDuration

  function handleSave() {
    if (newWorkDuration > 0 && newBreakDuration > 0) {
      dispatch('save', {
        workDuration: newWorkDuration,
        breakDuration: newBreakDuration,
      })
    }
  }

  function handleCancel() {
    dispatch('cancel')
  }
</script>

<div class="settings-overlay">
  <div class="settings-modal">
    <h2>⚙️ Configuración</h2>

    <div class="settings-group">
      <label for="workDuration">Duración de Trabajo (minutos)</label>
      <div class="input-group">
        <button
          class="decrement-btn"
          on:click={() => (newWorkDuration = Math.max(1, newWorkDuration - 1))}
        >
          −
        </button>
        <input
          id="workDuration"
          type="number"
          min="1"
          max="120"
          bind:value={newWorkDuration}
        />
        <button
          class="increment-btn"
          on:click={() => (newWorkDuration = Math.min(120, newWorkDuration + 1))}
        >
          +
        </button>
      </div>
    </div>

    <div class="settings-group">
      <label for="breakDuration">Duración de Descanso (minutos)</label>
      <div class="input-group">
        <button
          class="decrement-btn"
          on:click={() => (newBreakDuration = Math.max(1, newBreakDuration - 1))}
        >
          −
        </button>
        <input
          id="breakDuration"
          type="number"
          min="1"
          max="60"
          bind:value={newBreakDuration}
        />
        <button
          class="increment-btn"
          on:click={() => (newBreakDuration = Math.min(60, newBreakDuration + 1))}
        >
          +
        </button>
      </div>
    </div>

    <div class="settings-actions">
      <button class="btn-save" on:click={handleSave}>✅ Guardar</button>
      <button class="btn-cancel" on:click={handleCancel}>❌ Cancelar</button>
    </div>
  </div>
</div>

<style>
  .settings-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
    animation: fadeIn 0.3s ease;
  }

  @keyframes fadeIn {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }

  .settings-modal {
    background: white;
    border-radius: 20px;
    padding: 30px;
    max-width: 400px;
    width: 90%;
    box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
    animation: slideUp 0.3s ease;
  }

  @keyframes slideUp {
    from {
      transform: translateY(30px);
      opacity: 0;
    }
    to {
      transform: translateY(0);
      opacity: 1;
    }
  }

  .settings-modal h2 {
    text-align: center;
    color: #2c3e50;
    margin-bottom: 30px;
    font-size: 1.5rem;
  }

  .settings-group {
    margin-bottom: 25px;
  }

  .settings-group label {
    display: block;
    margin-bottom: 10px;
    color: #2c3e50;
    font-weight: 600;
    font-size: 0.95rem;
  }

  .input-group {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
  }

  .increment-btn,
  .decrement-btn {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    border: 2px solid #ff6b6b;
    background: white;
    color: #ff6b6b;
    cursor: pointer;
    font-size: 1.2rem;
    font-weight: bold;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .increment-btn:hover,
  .decrement-btn:hover {
    background: #ff6b6b;
    color: white;
    transform: scale(1.1);
  }

  .settings-group input {
    width: 80px;
    padding: 10px;
    border: 2px solid #e0e0e0;
    border-radius: 10px;
    font-size: 1.2rem;
    text-align: center;
    font-weight: 600;
    transition: all 0.3s ease;
  }

  .settings-group input:focus {
    outline: none;
    border-color: #ff6b6b;
    box-shadow: 0 0 0 3px rgba(255, 107, 107, 0.1);
  }

  .settings-actions {
    display: flex;
    gap: 15px;
    margin-top: 30px;
  }

  .btn-save,
  .btn-cancel {
    flex: 1;
    padding: 12px;
    border: none;
    border-radius: 10px;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
  }

  .btn-save {
    background: #ff6b6b;
    color: white;
  }

  .btn-save:hover {
    background: #ff5252;
    transform: translateY(-2px);
    box-shadow: 0 10px 20px rgba(255, 107, 107, 0.3);
  }

  .btn-cancel {
    background: #e0e0e0;
    color: #2c3e50;
  }

  .btn-cancel:hover {
    background: #d5d8dc;
    transform: translateY(-2px);
  }

  @media (max-width: 480px) {
    .settings-modal {
      padding: 20px;
    }

    .settings-modal h2 {
      font-size: 1.3rem;
      margin-bottom: 20px;
    }
  }
</style>
