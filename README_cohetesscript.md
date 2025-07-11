# 🚀 Sistema de Despliegue Interplanetario - Stellar Launcher

![Demo del Script](https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExcWJ0d2V6eGx0YzF0dWJjZ3BqZ2V6b2JtYzZ4NnA1aGZ6eHp1dSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/XgJew6mboozEWJ1Q7h/giphy.gif)

Un avanzado sistema de simulación de lanzamientos espaciales con animaciones ASCII y efectos de terminal.

## ✨ Características

- 🛰️ Simulación de 5 misiones espaciales únicas
- 🎨 Animaciones ASCII de cohetes en tiempo real
- ⏱️ Cuenta regresiva interactiva con efectos visuales
- 🌈 Colores ANSI personalizados para terminal
- 🚀 Efectos de "despegue" animados
- 📜 Citas inspiradoras de pioneros espaciales

## 🛠️ Requisitos

- Bash 4.0+ (`bash --version`)
- Terminal compatible con ANSI colors (GNOME Terminal, iTerm2, etc.)
- Linux/macOS (no probado en Windows Subsystem for Linux)

## 🚀 Cómo Usar

```bash
# 1. Clona el repositorio
git clone https://github.com/tuusuario/stellar-launcher.git
cd stellar-launcher

# 2. Dale permisos de ejecución
chmod +x info_cohetes.sh

# 3. Ejecuta el script
./info_cohetes.sh

📸 Capturas
https://example.com/screenshot1.png | https://example.com/screenshot2.png

🌌 Misiones Disponibles
Nombre Misión	Destino
Phoenix-7	Estación Alfa Centauri
Titan-Nova	Colonia Titán
Solaris-9	Órbita Solar
Nebula-One	Núcleo Galáctico
Quantum-X	Agujero de Gusano Θ-456


## Codigo.
#!/usr/bin/env bash
# stellar_launcher.sh — Sistema Avanzado de Despliegue Interplanetario

set -euo pipefail
IFS=$'\n\t'

# Configuración de misiones únicas
declare -A missions=(
  ["Phoenix-7"]="Estación Alfa Centauri"
  ["Titan-Nova"]="Colonia Titán"
  ["Solaris-9"]="Órbita Solar"
  ["Nebula-One"]="Núcleo Galáctico"
  ["Quantum-X"]="Agujero de Gusano Θ-456"
)

# Arte ASCII mejorado del cohete
declare -a rocket=(
    "    /\    "
    "   /  \   "
    "  /|  |\  "
    "  \|  |/  "
    "  /____\  "
    "  \    /  "
    "   \  /   "
    "    \/    "
    "    ||    "
    "    ||    "
    "    ||    "
    "   ====   "
)

# Colores ANSI mejorados
declare -A colors=(
    ["reset"]="\e[0m"
    ["title"]="\e[1;38;5;45m"
    ["countdown"]="\e[1;38;5;226m"
    ["success"]="\e[1;38;5;46m"
    ["mission"]="\e[1;38;5;51m"
    ["destination"]="\e[1;38;5;129m"
    ["flames"]="\e[38;5;202m"
)

# Función de espera optimizada
pause() {
    local secs=${1:-1}
    sleep "$secs" 2>/dev/null || sleep 1
}

# Limpiar pantalla de forma portable
clear_screen() {
    printf "\033[2J\033[H"
}

# Mostrar animación de despegue
animate_launch() {
    local frames=20
    local rocket_height=${#rocket[@]}
    
    for ((i=0; i<frames; i++)); do
        clear_screen
        
        # Espacio vacío antes del cohete
        for ((j=0; j<frames-i; j++)); do
            printf "\n"
        done
        
        # Cohete
        for line in "${rocket[@]}"; do
            printf "%s\n" "$line"
        done
        
        # Llamas animadas
        if ((i % 2 == 0)); then
            printf "${colors[flames]}    /\\    \n   /  \\   ${colors[reset]}\n"
        else
            printf "${colors[flames]}   /  \\   \n  /    \\  ${colors[reset]}\n"
        fi
        
        pause 0.08
    done
}

# Secuencia de lanzamiento
launch_sequence() {
    local mission=$1
    local destination=$2
    
    echo -e "\n${colors[title]}🛰  Iniciando ${colors[mission]}${mission}${colors[title]} hacia ${colors[destination]}${destination}${colors[reset]}"
    echo -e "${colors[title]}⏳ Inicializando sistemas...${colors[reset]}"
    pause 0.5
    
    # Verificación de sistemas
    for system in "Propulsión" "Navegación" "Comunicaciones" "IA de Vuelo"; do
        echo -e "  ✅ ${system}... \t[${colors[success]}OK${colors[reset]}]"
        pause 0.2
    done
    
    # Cuenta regresiva interactiva
    echo -e "\n${colors[title]}🚀 Secuencia de ignición iniciada:${colors[reset]}"
    for i in {5..1}; do
        printf "\r  T-${colors[countdown]}%02d${colors[reset]} segundos | Preparando motores..." "$i"
        pause 1
    done
    
    echo -e "\r  ${colors[success]}¡DESPEGUE!${colors[reset]}                          "
    animate_launch
    
    echo -e "\n${colors[success]}✔ Misión ${colors[mission]}${mission}${colors[success]} en curso hacia ${colors[destination]}${destination}${colors[reset]}\n"
    pause 0.8
}

main() {
    # Configuración de terminal
    tput civis
    clear_screen
    
    echo -e "${colors[title]}███████╗████████╗███████╗██╗     ██╗      █████╗ ██████╗ ███████╗██████╗ "
    echo -e "██╔════╝╚══██╔══╝██╔════╝██║     ██║     ██╔══██╗██╔══██╗██╔════╝██╔══██╗"
    echo -e "███████╗   ██║   █████╗  ██║     ██║     ███████║██████╔╝█████╗  ██████╔╝"
    echo -e "╚════██║   ██║   ██╔══╝  ██║     ██║     ██╔══██║██╔═══╝ ██╔══╝  ██╔══██╗"
    echo -e "███████║   ██║   ███████╗███████╗███████╗██║  ██║██║     ███████╗██║  ██║"
    echo -e "╚══════╝   ╚═╝   ╚══════╝╚══════╝╚══════╝╚═╝  ╚═╝╚═╝     ╚══════╝╚═╝  ╚═╝${colors[reset]}"
    echo -e "               SISTEMA DE LANZAMIENTO INTERESTELAR v3.2.1\n"
    
    for mission in "${!missions[@]}"; do
        launch_sequence "$mission" "${missions[$mission]}"
    done
    
    tput cnorm
    echo -e "${colors[title]}🎯 Todas las misiones desplegadas con éxito. ¡El futuro es ahora! 🌌${colors[reset]}"
    echo -e "${colors[destination]}«La humanidad no permanecerá en la Tierra para siempre» — Konstantin Tsiolkovsky${colors[reset]}\n"
}

main
EOF