# Barracuda X Battery en español

Aplicación para Windows 10 y 11 que muestra el nivel de batería de los Razer Barracuda X (2022) conectados mediante el receptor USB de 2,4 GHz.

## Abrir la versión portátil

1. Extrae todo el ZIP en una carpeta.
2. Conecta el receptor USB y enciende los audífonos.
3. Ejecuta `BarracudaBattery.exe` desde la carpeta extraída. La carpeta `_internal` contiene las dependencias de la aplicación.

La ventana usa Microsoft Edge WebView2. Al cerrarla, el icono de batería sigue en el área de notificación. Desde ahí puedes volver a abrir la ventana, actualizar la lectura o salir de la aplicación.

## Qué puedes consultar

- **Resumen**. Nivel actual, estado de carga, autonomía estimada y gráfico de las últimas 24 horas.
- **Historial y ciclos de carga**. Sesiones con batería y con cable, tiempo de uso y consumo entre cargas.
- **Uso y resumen semanal**. Uso por día y por hora, comparación con la semana anterior y estimación de salud de la batería.
- **Dispositivo**. Firmware, receptor, ecualizador de 10 bandas, modo No molestar, apagado automático e informe de diagnóstico.

El receptor YS-Tech (`1532:0550`) se probó en el proyecto original. El receptor Macronix (`1532:0552`) está implementado, pendiente de confirmación en hardware. Los registros se guardan en `%LOCALAPPDATA%\BarracudaBattery`.

## Compilar desde el código fuente

Con Python 3.13 o posterior e Inno Setup 6 instalados, ejecuta `python -m pip install -r requirements-dev.txt` y después `.\build.ps1` en PowerShell.

Proyecto original de [nightdevx](https://github.com/nightdevx/barracuda-x-battery). [Licencia MIT](LICENSE).

