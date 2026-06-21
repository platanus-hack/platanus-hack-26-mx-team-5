# MyEyesTalk — Puente

**Plataforma de accesibilidad audio-first para personas con discapacidad visual en México y LATAM, construida sobre las Ray-Ban Meta Gen 2.**

MyEyesTalk no sustituye los sentidos: **devuelve agencia**. Traduce lo que ven las gafas (punto de vista egocéntrico) en **narración espacial**, **decisiones** y **acciones por voz** a través de los altavoces de las gafas, sin pantalla ni HUD.

## El problema

Las personas ciegas o con baja visión en LATAM dependen de bastón, perro guía o asistencia humana para tareas cotidianas como navegar un supermercado, identificar productos o leer etiquetas. Los asistentes genéricos (incluido Meta AI) no aprenden el entorno, no manejan una lista de compras, no recuerdan marcas ni preferencias y no dan orientación espacial accionable en español mexicano.

## La solución

Un loop cognitivo que corre en el teléfono y usa las gafas solo como cámara + micrófono + altavoz:

```
Ray-Ban Meta Gen 2 (cámara + mic + speakers)
   ↔ App iOS nativa (Swift + MWDAT)
       ↔ Backend (Cloudflare Worker: visión + RAG + agente Hermes)
           → TTS de vuelta a los altavoces de las gafas
```

1. **Push-to-talk / Modo Sentido** → captura voz y frame POV.
2. **STT** (AssemblyAI) → transcripción.
3. **RAG** → si ya conoce el lugar, evita re-analizar (aprende el supermercado).
4. **Visión** (Claude / GPT-4o) → `SceneJSON` / `ProductJSON`.
5. **Agente Hermes** → decisión, lista de compras, alternativas de marca, recall.
6. **TTS** (ElevenLabs) → respuesta hablada y espacial por las gafas.

## Módulos

| Módulo | Función |
|--------|---------|
| **Sentido** | Orientación y narración espacial egocéntrica (izquierda / derecha / adelante). |
| **Puente** | Saludos, mensajes y confirmaciones por voz. |
| **Super** | Lista de compras + RAG del supermercado + identificación de productos. |
| **Mano** | Dictado y lectura de documentos. |
| **Calma** | Respuestas adaptativas según estado del usuario. |

## Diferenciador

A diferencia de un asistente genérico, MyEyesTalk es **egocéntrico y en español mexicano**, **aprende el entorno con RAG**, mantiene **lista y memoria** con patrones tipo Hermes, y confirma productos antes de actuar — todo demostrable en un flujo real de persona ciega en un supermercado (3 escenarios de visita).

## Stack

- **Gafas:** Ray-Ban Meta Gen 2 + DAT iOS (MWDAT)
- **App MVP:** `puente/apps/mobile-ios/` — Swift nativo
- **Backend:** Cloudflare Worker (rutas de fusión, RAG, agente, TTS, STT)
- **Visión:** Claude / GPT-4o mini → JSON estructurado
- **STT:** AssemblyAI · **TTS:** ElevenLabs · **Live:** Gemini Live API

## Estructura del repositorio

```
puente/      → código principal (app iOS, backend worker, prompts, schemas)
external/    → agentes y módulos de visión auxiliares
infra/       → experimentos de infraestructura local
*.md         → investigación, flujos y documentación de diseño
```

## Disclaimer

MyEyesTalk es un apoyo complementario. No sustituye bastón, perro guía, instrucción de orientación y movilidad ni certificaciones médicas.
