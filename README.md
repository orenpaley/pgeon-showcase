# Pgeon

Pgeon converts photographed chess scoresheets into structured chess notation and provides a board-based workflow for reviewing, correcting, editing, and exporting games as Portable Game Notation (PGN).

> **Beta:** Pgeon is independently developed and actively deployed. This repository contains its public technical case study. The production source code is maintained privately.

## Live application

[Open Pgeon](https://pgeon.app)

## Overview

Manually converting a handwritten chess scoresheet into PGN is slow and susceptible to notation errors.

Pgeon combines image extraction with deterministic chess-rule validation. Extracted moves are treated as candidates rather than final game data: each move passes through structured response validation and sequential legal-move review before becoming part of the game document.

## Workflow

```text
Upload → Prepare → Extract → Review → Edit → Export
```

1. Upload and crop a scoresheet image.
2. Normalize the image for extraction.
3. Extract structured candidate moves.
4. Validate each candidate against the current board position.
5. Pause for user correction when a move is uncertain or illegal.
6. Continue editing the accepted game on an interactive board.
7. Export the completed game as PGN.

## Core capabilities

### Image preparation

- File validation, cropping, and orientation handling
- Dimension and file-size normalization
- Visible preparation progress and recovery states

### Extraction and review

- Backend-controlled OpenAI API requests
- Structured response validation
- Sequential legal-move validation
- Automatic playback with pause, correction, and undo
- Explicit promotion handling

### PGN editing

- Legal move entry for both colors
- Main lines and nested variations
- Variation promotion and deletion
- Headers, comments, and annotations
- Board drawings and orientation
- PGN import and export

## Technology

| Area | Technology |
|---|---|
| Frontend | React, Vite, JavaScript |
| Backend | Python, FastAPI, Pydantic |
| Chess processing | `python-chess` |
| Extraction | OpenAI API |
| Testing | Vitest, React Testing Library, pytest |
| Deployment | Vercel, Railway |

## Architecture

For details, see [Architecture](/architecture.md).

## Engineering highlights

- Treats model output as untrusted candidate data
- Keeps extraction credentials and provider communication on the server
- Validates moves independently against the current chess position
- Maintains one canonical document for the board, move list, variations, and PGN
- Represents alternative continuations as a move tree
- Pauses for user input rather than silently guessing
- Protects critical workflows with automated frontend and backend tests

## Status

Pgeon is currently in beta.

## Author

Developed by Oren Paley.

- [GitHub](https://github.com/orenpaley)
- [Live application](https://pgeon.app)