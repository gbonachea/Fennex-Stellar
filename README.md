# Stellar Fox

Navegador web moderno para Linux hecho en **C++17 + Qt6**, con interfaz
inspirada en los navegadores móviles: las pestañas se gestionan desde un
**botón de pestañas** en la barra inferior que muestra una cuadrícula visual
de miniaturas, igual que Chrome/Firefox en Android/iOS.

<img width="1366" height="732" alt="fennex-stellar" src="https://github.com/user-attachments/assets/89c8783a-30b2-498a-bcf7-4d1c0af964f0" />

---

## Características

| Función | Detalle |
|---|---|
| **Vista de pestañas** | Cuadrícula de tarjetas con miniatura, título y favicon |
| **Barra inferior** | Estilo móvil: atrás, adelante, recargar, inicio, pestañas |
| **Barra de direcciones** | Muestra solo el host en reposo, URL completa al enfocar |
| **Motor de renderizado** | Chromium vía `QWebEngineView` (Qt6 WebEngine) |
| **Descargas** | Gestor integrado con diálogo de guardado |
| **Marcadores** | Agregar/ver con botón ☆ |
| **Historial** | Registro automático de navegación |
| **Configuración** | Diálogo con privacidad, zoom y buscador predeterminado |
| **Buscar en página** | Barra Find (Ctrl+F) |
| **Impresión** | Ctrl+P |
| **Tema** | Catppuccin Mocha (oscuro) |
| **Animaciones** | Transición suave al abrir/cerrar la vista de pestañas |

---

## Requisitos

- **Linux** (x86_64)  
- **Qt 6.4+** con módulos: `QtWidgets`, `QtWebEngineWidgets`, `QtNetwork`, `QtPrintSupport`  
- **CMake 3.16+**  
- **C++17** compatible: `g++ 10+` o `clang++ 12+`

### Ubuntu / Debian

```bash
sudo apt install -y cmake ninja-build g++ \
    qt6-base-dev qt6-webengine-dev qt6-webengine-dev-tools \
    libqt6webenginewidgets6 libqt6webenginecore6 libgl1-mesa-dev
```

### Arch Linux

```bash
sudo pacman -S cmake ninja qt6-base qt6-webengine gcc
```

### Fedora

```bash
sudo dnf install cmake ninja-build gcc-c++ qt6-qtbase-devel qt6-qtwebengine-devel
```

---

## Compilar e instalar

```bash
# Clonar / extraer el proyecto
cd flow-browser

# Script automático (detecta distro e instala deps si se necesita)
chmod +x install.sh
./install.sh

# O manualmente:
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
make -j$(nproc)
./StellarFox
```

---

## Estructura del proyecto

```
flow-browser/
├── CMakeLists.txt
├── install.sh
├── README.md
├── resources/
│   ├── resources.qrc
│   └── icons/app.png
└── src/
    ├── main.cpp              # Punto de entrada, paleta oscura
    ├── MainWindow.h/cpp      # Ventana principal, gestión de tabs
    ├── BrowserTab.h/cpp      # Pestaña individual (QWebEngineView + FindBar)
    ├── TabOverview.h/cpp     # Cuadrícula de pestañas (overlay)
    ├── TabThumbnail.h/cpp    # Tarjeta individual con miniatura
    ├── ToolBar.h/cpp         # Barra inferior (barra de nav + dirección)
    ├── AddressBar.h/cpp      # Campo de URL inteligente
    ├── DownloadManager.h/cpp # Gestión de descargas
    ├── BookmarkManager.h/cpp # Marcadores + Historial
    └── SettingsDialog.h/cpp  # Configuración
```

---

## Atajos de teclado

| Atajo | Acción |
|---|---|
| `Ctrl+T` | Nueva pestaña |
| `Ctrl+W` | Cerrar pestaña actual |
| `Ctrl+Tab` | Siguiente pestaña |
| `Ctrl+L` | Enfocar barra de direcciones |
| `Ctrl+F` | Buscar en página |
| `Ctrl+R` / `F5` | Recargar |
| `Ctrl++` / `Ctrl+-` | Zoom +/- |
| `Ctrl+0` | Resetear zoom |
| `Ctrl+P` | Imprimir |
| `Escape` | Cerrar vista de pestañas |

---

## Personalización

El tema se basa en variables de color definidas en los stylesheets de Qt.
Para cambiar el esquema de colores, busca las constantes hexadecimales en
`ToolBar.cpp`, `TabOverview.cpp` y `TabThumbnail.cpp`:

| Variable | Color | Uso |
|---|---|---|
| `#1e1e2e` | Fondo base | Fondo principal |
| `#12121c` | Fondo oscuro | Barra de herramientas |
| `#24273a` | Superficie | Tarjetas, inputs |
| `#cdd6f4` | Texto principal | Labels, URLs |
| `#89b4fa` | Acento azul | Botones, tab activa |
| `#cba6f7` | Acento morado | Gradientes |

---

## Licencia

MIT — libre para modificar y distribuir.
