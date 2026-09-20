# SoulDub AI Video Translation Skill for AI Agents

[English](README.md) | [简体中文](README.zh-CN.md) | [Español](README.es.md) | [ไทย](README.th.md)

Traduce vídeos MP4 locales con la traducción de vídeo y el doblaje con voz original de SoulDub AI. Después, descarga el vídeo traducido, los subtítulos en el idioma de destino y los subtítulos SRT bilingües.

Este repositorio publica el Agent Skill `souldub-video-translate`.

Úsalo cuando quieras que un agente localice un vídeo MP4, lo doble a otro idioma, traduzca sus subtítulos o genere subtítulos bilingües para revisarlos.

## Funciones

El skill ayuda al agente a:

- Subir un vídeo `.mp4` local a SoulDub.
- Crear una tarea de traducción de vídeo.
- Seguir el progreso de una traducción de larga duración.
- Descargar el vídeo traducido con doblaje de IA y los subtítulos SRT.

Las ejecuciones completadas guardan:

- `result.mp4`: vídeo traducido
- `translated.srt`: subtítulos en el idioma de destino
- `bilingual.srt`: subtítulos bilingües

## Instalación

Instálalo desde el repositorio público de GitHub:

```bash
npx skills add jiabaogithub/souldub-skills --skill souldub-video-translate
```

## Uso

Después de instalarlo, pide al agente que use el skill con la ruta de un MP4 local y un idioma de destino:

```text
Usa el skill souldub-video-translate para traducir C:\path\to\video.mp4 al japonés.
```

Otros ejemplos:

```text
Usa el skill souldub-video-translate para doblar este MP4 al chino.
Usa el skill souldub-video-translate para localizar este vídeo y generar subtítulos bilingües.
```

El skill también acepta nombres de idiomas como `Japanese`, `Chinese`, `日语`, `中文` y `粤语`.

El agente solicitará los datos que falten, iniciará la traducción, informará del progreso y devolverá las rutas locales de los archivos cuando termine.

## Configuración

El skill requiere una clave de API de SoulDub.

Después de instalarlo, pide al agente que compruebe la autenticación:

```bash
uv run scripts/video_translation.py auth status
```

Si no hay una clave configurada, el skill crea este archivo de configuración del usuario:

```text
~/.souldub/souldub.config.yaml
```

Define `souldub_api_key` en ese archivo o establece la variable de entorno `SOULDUB_API_KEY`.

## Requisitos

- Python 3.11+
- `uv`
- Acceso de red a la API de SoulDub Agent
- Una clave de API de SoulDub
- Permiso de lectura del MP4 de origen
- Permiso de escritura en el directorio de salida

## Datos de ejecución y seguridad

Los archivos del skill instalado se tratan como de solo lectura.

El estado de ejecución se guarda en el directorio de estado de la plataforma del usuario. Los resultados traducidos se guardan por defecto en una carpeta `souldub_outputs/` junto al vídeo de origen.

El skill no guarda de forma persistente claves de API, URL de carga prefirmadas, URL de la pasarela multimedia ni parámetros de firma temporales.

## Desarrollo

Estructura del repositorio:

```text
skills/
└── souldub-video-translate/
```

Desde la raíz del repositorio, comprueba el descubrimiento local:

```bash
npx skills add . --list
```

Instala la copia de trabajo local:

```bash
npx skills add . --skill souldub-video-translate
```

Ejecuta directamente el script auxiliar para depuración local:

```bash
cd skills/souldub-video-translate
uv run scripts/video_translation.py auth status
```
