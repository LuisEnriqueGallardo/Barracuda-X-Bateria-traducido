<div align="center">

<img src="assets/logo.png" width="96" alt="">

# Barracuda X Battery

**Nivel de batería, historial y ajustes para los auriculares Razer Barracuda X (2022) en Windows — a través de su receptor USB de 2,4 GHz, donde Windows no muestra nada.**

[![Download](https://img.shields.io/github/v/release/nightdevx/barracuda-x-battery?label=original)](https://github.com/nightdevx/barracuda-x-battery/releases/latest)
[![Platform](https://img.shields.io/badge/platform-Windows%2010%20%2F%2011-0078D4)](#install)
[![Python](https://img.shields.io/badge/python-3.13%2B-3776AB)](#development)
[![UI](https://img.shields.io/badge/UI-WebView2-2C7BE5)](#how-it-works)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

**Traducción al español para Windows** del [proyecto de nightdevx](https://github.com/nightdevx/barracuda-x-battery) para los Razer Barracuda X (2022). Este proyecto es independiente y no tiene relación oficial con Razer. Se conserva la [licencia MIT original](LICENSE).

[Descarga el ejecutable en Releases](https://github.com/LuisEnriqueGallardo/Barracuda-X-Bateria-traducido/releases/latest) y abre `BarracudaBattery-ES.exe`. También está disponible la versión portátil en ZIP. [Guía en español](README.es.md).

**English** · [Türkçe](README.tr.md) · [Español](README.es.md)

<img src="docs/images/overview.png" width="900" alt="Overview page">

</div>

---

Por Bluetooth, Windows muestra la batería de los Barracuda X. Por el receptor de 2,4 GHz no muestra nada, y el
software de escritorio de Razer no es compatible con estos auriculares en absoluto: el nivel, el ecualizador y el
temporizador de espera solo están disponibles en la app del teléfono.

Esta aplicación se comunica con el receptor directamente por HID. Mantiene el nivel en el área de notificación,
registra una lectura cada minuto, convierte el registro en historial, ciclos de carga y estadísticas de uso, y
cambia los ajustes de los auriculares desde la PC.

## Features

<table>
<tr>
<td width="55%" valign="top">

**Nivel en el área de notificación.** El propio porcentaje es el ícono de la bandeja; mientras carga aparece sobre una
insignia de color. Notificación de batería baja al 20 %.

**La carga aparece al instante.** Los auriculares reportan por sí mismos los cambios de cable y batería; la app los
detecta y lee en dos segundos en lugar de esperar al siguiente sondeo.

**Historial.** Nivel de batería en 24 horas, 7 días, 30 días o todo el historial, tramos cargando y con batería en
sus propios colores, y cada sesión en una tabla.

**Ciclos de carga.** Desde desconectar hasta volver a conectar: horas de uso, cuánto bajó la batería y cuánto dura una
carga completa a ese ritmo.

**Uso y resumen semanal.** Horas por día, un dato semanal de duración a carga completa que muestra el desgaste de la
batería, ciclos completos equivalentes y una vista semana a semana comparada con la anterior.

**Ajustes de los auriculares.** Perfiles de ecualizador, ecualizador personalizado de 10 bandas, no molestar y
apagado automático. Cada cambio se vuelve a leer desde los auriculares antes de darse por válido.

**Estética estilo Razer.** Negro, verde neón, paneles biselados, tipografía condensada en mayúsculas y un anillo de
batería segmentado, para encajar junto al resto de un setup Razer.

</td>
<td width="45%" valign="top">

<img src="docs/images/cycles.png" width="100%" alt="Charge cycles page">

</td>
</tr>
</table>

### Screens

| History | Usage | Weekly summary |
|---|---|---|
| <img src="docs/images/history.png" alt="History page"> | <img src="docs/images/usage.png" alt="Usage page"> | <img src="docs/images/week.png" alt="Weekly summary page"> |
| Nivel en el tiempo, sesiones, tasa de descarga y tiempo con batería. | Horas diarias, duración a carga completa por semana, salud de la batería. | Una semana frente a la anterior. |

| Headset settings | |
|---|---|
| <img src="docs/images/device.png" alt="Device page"> | Firmware, receptor, perfiles de EQ, ecualizador personalizado de 10 bandas, no molestar y apagado automático. Cada cambio se vuelve a leer desde los auriculares; si no lo aplica, vuelve a mostrarse el valor anterior en pantalla. |

## Install

Descarga `BarracudaBattery-Setup-<version>.exe` desde los [releases del proyecto original](https://github.com/nightdevx/barracuda-x-battery/releases/latest) y ejecútalo. Para la compilación en español, usa el [release portátil](../../releases/latest).

- No requiere permisos de administrador. Se instala por usuario en `%LOCALAPPDATA%\Programs\BarracudaBattery`.
- No requiere Python; el entorno de ejecución viene incluido.
- La ventana usa Microsoft Edge WebView2, incluido en Windows 11.
- El instalador cierra una copia anterior si está abierta y puede iniciar la app con Windows (activado por defecto).
- Instalador de 17 MB, ~41 MB instalado.

> **SmartScreen.** El instalador no está firmado digitalmente, por lo que Windows advertirá la primera vez: **Más información → Ejecutar de todas formas**.

Desinstala desde Configuración → Aplicaciones. El registro permanece en `%LOCALAPPDATA%\BarracudaBattery`; elimina esa carpeta si también quieres borrarlo.

Esta copia incluye una interfaz en español. Consulta la [guía en español](README.es.md) para la compilación localizada.

## Supported hardware

| Receiver (USB id) | Headset | Status |
|---|---|---|
| `1532:0550` (YS-Tech bridge) | Barracuda X (2022) | Probado: batería, cable, eventos y todos los ajustes |
| `1532:0552` (Macronix bridge) | Barracuda X (2022) | Implementado a partir de notas del protocolo publicadas; aún no confirmado en hardware |
| `1532:0536`, `1532:0574` | Barracuda X (2021), Barracuda X Chroma | No compatible; la app identifica el receptor y lo indica |

Los Barracuda X (2022) se venden con cualquiera de los dos receptores, y ambos envían los mismos comandos a los
auriculares. Por Bluetooth el receptor no puede comunicarse con los auriculares; ese caso lo cubre el propio indicador
de batería de Windows.

Si tienes un `0552` y algo no funciona, abre **Dispositivo → Informe de diagnóstico** y adjunta el archivo
`tanilama.txt` que guarda en un *issue*. Lista las interfaces HID que ve Windows y el tráfico sin procesar de una
lectura.

## How it works

El receptor hace de puente entre USB HID y el chip Airoha de los auriculares. Cada comunicación cambia el receptor
para reenviar comandos (`E1 01`), envía comandos de datos de cliente de Airoha (`50 41 08 …`) — porcentaje de
batería `21`, cable `2A`, perfil de EQ `13`, EQ personalizado `15`, no molestar `27`, espera `2C` — y lo devuelve a
su estado anterior. Al fijar un valor, se vuelve a leer para comprobarlo. Las dos versiones del receptor solo se
diferencian en el entramado HID alrededor de esos comandos:

| | YS-Tech (`0550`) | Macronix (`0552`) |
|---|---|---|
| Report id | `02` | `01` |
| Out | `02 80 len crc crc` + comando, CRC-16/XMODEM | `01 80 len` + comando, tras un apretón de manos `01 40` |
| Accepted | `GetInputReport`: `O` taken, `F` busy | — |
| In | `02 len` + tramas | `01 80 len` + tramas; una trama puede abarcar varios reportes |

La aplicación se ejecuta como dos procesos desde un mismo programa:

| Process | Does | Memory |
|---|---|---|
| Tray (`--tray` at sign-in) | Lee cada minuto y ante eventos de los auriculares, registra datos, ícono en bandeja y notificaciones. Sin interfaz gráfica pesada. | ~33 MB private |
| Window (`--ui`, started from the tray) | La página HTML en WebView2: lee el registro, lee y escribe ajustes. | ~73 MB + WebView2, solo mientras está abierta |

WebView2 mantiene alrededor de 300 MB incluso con la ventana oculta, por lo que cerrar la ventana finaliza ese
proceso en lugar de ocultarlo. Un *mutex* con nombre serializa el acceso al receptor entre ambos procesos; el
registro es SQLite en modo WAL, escrito por la bandeja y leído por la ventana.
