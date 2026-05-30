<div align="center">

<img src="assets/vector-logo.png" alt="Vector Voice" width="200"/>

# Vector Voice

**Голосовой слой экосистемы Vector — STT, TTS, intent recognition, diarization. On-device, без облака.**

[![Hermes Agent](https://img.shields.io/badge/Hermes-Agent-blue.svg)](https://github.com/NousResearch/hermes-agent)
[![Powered by Moonshine](https://img.shields.io/badge/Powered%20by-Moonshine-green.svg)](https://github.com/moonshine-ai/moonshine)
[![Models: 26MB–top](https://img.shields.io/badge/Models-26MB–top-orange.svg)](#модели)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

</div>

---

Голосовой слой для всех виртуальных работников Vector. Единая библиотека: STT (выше Whisper Large V3), TTS (русский язык), intent recognition (семантический matching), diarization (кто говорит). Всё on-device, без API-ключей.

## Установка

```bash
pip install moonshine-voice
```

## Быстрый старт

```bash
# Транскрипция с микрофона
python -m moonshine_voice.mic_transcriber --language ru

# Распознавание команд
python -m moonshine_voice.intent_recognizer

# Синтез речи
python -m moonshine_voice.tts --language ru --text "Привет, я Vector Voice"
```

## Модели

| Модель | Размер | Для чего |
|--------|--------|---------|
| tiny | 26 МБ | Raspberry Pi, IoT, constrained |
| small | ~100 МБ | Десктоп, быстрый отклик |
| base | ~300 МБ | Баланс точности и скорости |
| large | ~1.5 ГБ | Максимальная точность |

## Кто использует

| Проект | Для чего |
|--------|---------|
| **Vector Home** | Голосовое управление умным домом: «включи свет на кухне» |
| **Vector Meat** | Голосовые отчёты смены, диктовка показателей |
| **Vector Marketing** | Транскрипция звонков, голосовые заметки |
| **Vector Work** | Голосовой ввод задач, диктовка документов |

## Интеграция с Vector Home

```python
from moonshine_voice import MicTranscriber, IntentRecognizer
from vector_home import HA_Bridge

# Слушаем и понимаем
transcriber = MicTranscriber(language="ru")
recognizer = IntentRecognizer()

for text in transcriber.stream():
    intent = recognizer.match(text, actions=[
        "включи свет", "выключи свет",
        "открой шторы", "закрой шторы",
        "какая температура"
    ])
    if intent:
        HA_Bridge.execute(intent)
```

## Что заменяет

| Старый стек | Новый стек |
|------------|-----------|
| Whisper (STT) | Moonshine STT — выше точность, ниже задержка |
| Piper (TTS) | Moonshine TTS — русский из коробки |
| GPT-2 router (intent) | Moonshine Intent — семантический matching |

Одна библиотека вместо трёх. `pip install moonshine-voice` — и всё работает.

## Источник

На базе [Moonshine Voice](https://github.com/moonshine-ai/moonshine) — 8.3K+ звёзд, C, on-device.
