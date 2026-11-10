# Conchy WM (`conchy-wm`)

High-performance, opinionated scrollable-tiling Wayland compositor for **Conchy OS** (`github.com/conchy-os`), written in 100% Rust on top of [Smithay](https://github.com/Smithay/smithay).

---

## 🧭 Key Features & Principles

- **Scrolling-first (ленточный тайлинг):** Бесконечная горизонтальная лента колонок — эргономичная организация рабочего пространства для современных дисплеев и ультрабуков.
- **Hardware HDR & Color Management:**
  - Полная поддержка протоколов `wp_color_management_v1` и `frog_color_management_v1`.
  - Готовность к OLED панелям высокой плотности (3.1K) и HDR-рендерингу в Wine/Proton.
  - Управление яркостью SDR-контента на HDR-экранах и peak luminance override.
- **Explicit Sync & Ultra-Low Latency:**
  - Поддержка `linux-drm-syncobj-v1` (явная синхронизация) — устранение статтеров на GPU Intel Xe, AMD и NVIDIA.
  - Поддержка `wp_tearing_control_v1` (асинхронные pageflips) и прямой скан-аут (Direct Scanout) для максимальной отзывчивости в играх.
- **Vulkan & GLES Renderer:**
  - Аппаратное размытие фона (blur), скругление углов, градиентные рамки и кастомные шейдеры на Vulkan и GLES пайплайнах.
- **Native Minimizing:**
  - Нативное сворачивание окон (`Action::MinimizeWindow`, `Action::ToggleWindowMinimized`) с интеграцией в `conchy-shell` / док.
- **Void Linux First:**
  - Независимость от `systemd`: сессионная диспетчеризация через `conchy-session`.
  - Управление через сокет `$CONCHY_SOCKET` и IPC-крейт `conchy-ipc`.

---

## 📂 Структура крейтов

```
compositor/
├── src/                  # Ядро композитора (conchy-wm бинарник и библиотека)
├── conchy-ipc/           # Типобезопасная библиотека протокола IPC и CLI-клиент
├── conchy-wm-config/     # Парсер и структуры конфигурации KDL (~/.config/conchy/wm.kdl)
├── conchy-visual-tests/  # Визуальные регрессионные тесты
└── resources/            # Шаблоны конфигурации и порталов рабочего стола
```

---

## ⚙️ Конфигурация

Основной конфигурационный файл: **`~/.config/conchy/wm.kdl`**  
Системный шаблон: **`/etc/conchy/wm.kdl`**

Переменные окружения:
- `CONCHY_SOCKET` — путь к активному UNIX-сокету IPC (с обратной совместимостью с `NIRI_SOCKET`).
- `CONCHY_CONFIG` — путь к кастомному конфигурационному файлу (с обратной совместимостью с `NIRI_CONFIG`).

---

## 🚀 Сборка и запуск

### Сборка
```bash
cargo build --release
```

### Запуск во вложенном окне (для разработки)
```bash
../scripts/run-nested.sh
```

### Управление через IPC
```bash
conchy-wm msg outputs
conchy-wm msg workspaces
conchy-wm msg windows
conchy-wm msg action focus-column-right
```

---

## 📄 Лицензия

GPL-3.0-or-later
