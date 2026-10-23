# 00 · Análisis de rea (morluto/rea)

Fecha de análisis: 2026-10-23 · Commit base upstream: `8c4f96ef4` (4.484 commits).

## Licencia
- **MIT** (`LICENSE`, © 2026 morluto).
- Permite: uso, copia, modificación, fusión, publicación, distribución, sublicencia y venta.
- Uso privado y comercial: permitidos.
- Obligación única: conservar el aviso de copyright y la licencia en copias o partes sustanciales.
- Sin garantía ni responsabilidad del autor.
- Ojo: `THIRD_PARTY_NOTICES.md` y `licenses/` recogen licencias de dependencias y código vendorizado (`third_party/`), que siguen sus propios términos.
- `DISCLAIMER.md` limita el uso aceptable: no DRM/licencias, no copiar software propietario, solo objetivos propios o autorizados.

## Propósito
- "REA: Reverse Engineer Anything": servidor **MCP** y CLI para que un agente de IA analice binarios, apps y comportamiento en runtime sin código fuente.
- Devuelve hallazgos con **evidencia, procedencia y "unknowns"** explícitos (observación ≠ inferencia).
- Paquete npm `rea-agents` v6.7.0; `npx rea-agents setup` lo registra en Claude Code, Codex, Cursor, Gemini CLI, etc.

## Stack
- TypeScript (ESM), Node.js ≥22.23.4 / 24.22.1 / 26.12.1; npm 11; Turbo; Vitest; Stryker (mutation testing); knip; jscpd.
- SDK MCP `@modelcontextprotocol/server|client` 2.3.1; transporte stdio (por defecto) o streamable HTTP.
- Parsers: Babel, parse5, saxes, protobuf, msgpack, cborg, stream-json; Playwright-core (browser/CDP).
- Bridges externos: Python (Hopper, Cutter, pwntools/pwndbg, mitmproxy, LLDB), Java (Ghidra HeadlessScript), Swift (macOS UI/procesos), Node-API C++ (Windows).
- Proveedores BYO: Hopper, Ghidra, IDA, JADX, rizin, GDB, objdump, Binwalk/Unblob, WABT, Frida.

## Arquitectura (`docs/architecture.mermaid`, `AGENTS.md`)
- Dependencias hacia dentro: `src/domain` (semántica/contratos) → adaptadores de proveedor → `src/application` (workflows compartidos) → adaptadores CLI (`src/cli`) y MCP (`src/server`, `src/main`).
- `src/composition`: factorías tipadas de proveedores y sesiones.
- `src/contracts`: esquemas visibles para el llamador (JSON Schema validados con ajv).
- `src/process`: supervisión de procesos propios, deadlines, lecturas acotadas, limpieza.
- Investigación: `EvidenceLedger`, `InvestigationRecords`, snapshots cacheados.
- Módulos por objetivo: `ghidra`, `hopper`, `ida`, `dotnet`, `javascript`, `electron`, `browser`, `android`, `firmware`, `wasm`, `evm`, `sqlite`, `pcap`, `model` (GGUF/safetensors), `gpu`, `il2cpp`, etc.
- Tamaño: ~886 ficheros TS en `domain`, ~461 en `application`, ~170 en `browser`.

## Cómo se ejecuta
```bash
npm ci
npm run build          # turbo artifacts:skills
npm run check:fast     # typecheck + lint
npx rea-agents setup   # registra el MCP en tu agente
rea analyze-javascript-application /abs/path --json
rea mcp                # servidor MCP stdio; `rea mcp --http` opcional
```
- Entrada: `scripts/rea.mjs` enruta a MCP o comando one-shot.

## Relevancia para este repo
- [Inferencia] rea **no** tiene nada de visión artificial ni de construcción; su valor aquí es como **framework de agente+evidencia** (MCP, ledger de evidencias, contratos tipados) reutilizable para una capa de análisis de obra.
- Restricción: rea **no** se usará contra software propietario de Buildots (DISCLAIMER + alcance de esta investigación).
