# 🍅 Pomodoro Screen - Aplicación de Escritorio

Una moderna aplicación Pomodoro construida con **Svelte** y **Tauri** que crea una experiencia visual inmersiva con un efecto de atardecer que oscurece la pantalla a medida que progresa tu sesión de trabajo.

## ✨ Características

- 🌅 **Efecto de atardecer visual** - Transición de colores realista que oscurece la pantalla (azul cielo → naranja → rojo → azul noche)
- ⏱️ **Timer configurable** - Trabajo: 50 minutos (por defecto), Descanso: 10 minutos (por defecto)
- 📊 **Estadísticas en tiempo real** - Seguimiento de sesiones completadas y tiempo total
- ⚙️ **Panel de configuración** - Personaliza duraciones de trabajo y descanso
- 🎨 **Interfaz moderna** - Diseño responsive con animaciones suaves
- 🖥️ **Aplicación de escritorio** - Construida con Tauri para máximo rendimiento
- 🎯 **Transiciones suaves** - Animaciones fluidas gracias a Svelte y CSS3

## 🚀 Instalación

### Requisitos Previos

- Node.js 16+
- Rust (para compilar Tauri)
- npm o yarn

### Pasos

```bash
# Clonar el repositorio
git clone https://github.com/LindaChocolatina/Pomodoro-screen.git
cd Pomodoro-screen

# Instalar dependencias
npm install
```

## 🏃 Uso

### Desarrollo

```bash
# Iniciar servidor de desarrollo
npm run dev

# En otra terminal, iniciar Tauri en desarrollo
npm run tauri-dev
```

### Compilación para Producción

```bash
# Compilar la aplicación
npm run tauri-build
```

## 📁 Estructura del Proyecto

```
Pomodoro-screen/
├── src/
│   ├── components/
│   │   ├── PomodoroTimer.svelte      # Componente principal del timer
│   │   ├── SunsetOverlay.svelte      # Efecto visual de atardecer
│   │   ├── SessionStats.svelte        # Estadísticas de sesiones
│   │   └── SettingsPanel.svelte       # Panel de configuración
│   ├── App.svelte                      # Componente raíz
│   └── main.js                         # Punto de entrada
├── src-tauri/                          # Código de Tauri
├── index.html                          # HTML principal
├── vite.config.js                      # Configuración de Vite
├── package.json                        # Dependencias del proyecto
└── README.md                           # Este archivo
```

## 🎯 Cómo Usar

1. **Iniciar sesión**: Haz clic en el botón "▶️ Iniciar" para comenzar el temporizador
2. **Pausar**: Pausa cuando sea necesario con el botón "⏸️ Pausar"
3. **Saltar**: Ve a la siguiente sesión con el botón "⏭️ Saltar"
4. **Reiniciar**: Vuelve a empezar con el botón "🔄 Reiniciar"
5. **Configurar**: Personaliza las duraciones en el panel "⚙️ Configuración"

### Efecto Visual

A medida que avanza tu sesión de trabajo, la pantalla experimenta una transformación visual:

- **0-25%**: Cielo azul → Tonos naranjas
- **25-50%**: Naranja → Rojo oscuro
- **50-75%**: Rojo oscuro → Púrpura
- **75-100%**: Púrpura → Azul noche

Este efecto crea una experiencia inmersiva que te ayuda a visualizar el progreso de tu trabajo.

## 🛠️ Tecnologías Utilizadas

- **Svelte 4** - Framework UI reactivo y eficiente
- **Tauri** - Framework de aplicaciones de escritorio
- **Vite** - Bundler moderno y rápido
- **CSS3** - Animaciones y transiciones suaves

## 📋 Técnica Pomodoro

La técnica Pomodoro es un método de gestión del tiempo basado en:
- 50 minutos de trabajo concentrado (configurable)
- 10 minutos de descanso (configurable)
- Después de 4 ciclos, un descanso más largo

Esta aplicación te ayuda a implementar esta técnica de manera visual e inmersiva.

## 📝 Licencia

Este proyecto está bajo la Licencia MIT.

## 👩‍💻 Autor

Creado por Linda Chocolatina

---

¡Aumenta tu productividad con el Pomodoro Screen! 🌅
