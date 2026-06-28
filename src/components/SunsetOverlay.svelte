<script>
  export let progress = 0
  export let isWorkSession = true

  // Colores del atardecer que evolucionan con el progreso
  function getSunsetColor(prog) {
    // Progresión: Azul cielo -> Naranja -> Rojo oscuro -> Azul oscuro
    if (prog < 25) {
      // Azul cielo a naranja
      const t = prog / 25
      const r = Math.round(135 + (255 - 135) * t)
      const g = Math.round(206 + (140 - 206) * t)
      const b = Math.round(235 + (0 - 235) * t)
      return `rgb(${r}, ${g}, ${b})`
    } else if (prog < 50) {
      // Naranja a rojo oscuro
      const t = (prog - 25) / 25
      const r = Math.round(255)
      const g = Math.round(140 + (60 - 140) * t)
      const b = Math.round(0 + (20 - 0) * t)
      return `rgb(${r}, ${g}, ${b})`
    } else if (prog < 75) {
      // Rojo oscuro a púrpura oscuro
      const t = (prog - 50) / 25
      const r = Math.round(255 + (50 - 255) * t)
      const g = Math.round(60 + (20 - 60) * t)
      const b = Math.round(20 + (50 - 20) * t)
      return `rgb(${r}, ${g}, ${b})`
    } else {
      // Púrpura oscuro a azul noche
      const t = (prog - 75) / 25
      const r = Math.round(50 + (20 - 50) * t)
      const g = Math.round(20 + (10 - 20) * t)
      const b = Math.round(50 + (40 - 50) * t)
      return `rgb(${r}, ${g}, ${b})`
    }
  }

  // Opacidad que aumenta con el progreso
  function getOpacity(prog) {
    return Math.min(prog / 100 * 0.8, 0.8)
  }

  $: sunsetColor = getSunsetColor(progress)
  $: opacity = getOpacity(progress)
</script>

<div
  class="sunset-overlay"
  style="background-color: {sunsetColor}; opacity: {opacity};"
  class:work={isWorkSession}
  class:break={!isWorkSession}
/>

<style>
  .sunset-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    pointer-events: none;
    transition: background-color 0.5s ease, opacity 0.5s ease;
    z-index: 1;
  }

  .sunset-overlay.work {
    animation: sunsetPulse 3s ease-in-out infinite;
  }

  .sunset-overlay.break {
    animation: none;
  }

  @keyframes sunsetPulse {
    0%,
    100% {
      filter: brightness(1);
    }
    50% {
      filter: brightness(1.05);
    }
  }
</style>
