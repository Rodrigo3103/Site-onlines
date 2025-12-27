# AI Coding Agent Instructions for PONTO PRO

## Project Overview

PONTO PRO is a single-file web application (`index.html`) for employee time tracking using Firebase Realtime Database. It manages employee records, time punches, and generates reports.

## Architecture

- **Single HTML file** with embedded CSS/JS - no build process required
- **Firebase integration**: Real-time database for employee data and time logs
- **Data structure**: Employees stored as `/funcionarios/{id}` with `historico` object keyed by ISO dates (e.g., `2025-12-27`)
- **Status logic**: `VAZIO` (no punches), `PENDENTE` (odd punches, open shift), `FECHADO` (even punches, closed shift)

## Key Components

- **Dashboard cards**: Display counts for total, completed, pending, and unstarted employees
- **Presence panel**: Real-time grid showing current employee status (ATIVO/PAUSA/OFF) with colored badges
- **CRUD form**: Add/edit employees (nome, funcao, placa, observacao) - all inputs converted to uppercase
- **Data table**: Sortable employee list with punch history, total time, and action buttons
- **Modal editing**: Manual time entry editing with comma-separated format (e.g., "08:00, 12:00, 13:00, 18:00")

## Coding Patterns

- **Input masks**: License plate auto-formats to `ABC-1234`; time inputs use `HH:MM` with colon insertion
- **Time calculations**: Pairwise subtraction of entry/exit times using `new Date()` objects
- **Real-time sync**: Use `db.ref("funcionarios").on("value")` for live updates
- **Admin protection**: Wrap sensitive actions (delete, import, backup) with `validarGestor(callback)`
- **Export formats**: CSV for Excel, PDF tables via jsPDF, JSON for backups
- **Theming**: CSS variables for light/dark mode toggling

## Data Flows

- Employee additions/edits trigger `salvarEDraw()` to push to Firebase
- Time punches append to `historico[dataSelecionadaISO].marcacoes` array
- Filtering/search updates table rendering without database queries
- Reports iterate over `dadosFuncionarios` array with date-specific `historico` lookups

## Integration Points

- **Firebase config**: Hardcoded in script tag - update for different projects
- **External libraries**: Firebase JS SDK (v9.17.1), jsPDF (v2.5.1) with autotable plugin
- **Local storage**: Password management for admin features

## Development Workflow

- Open `index.html` directly in browser - no server or build tools needed
- Test Firebase connectivity by checking console for initialization errors
- Use browser dev tools for debugging real-time data changes
- Export features rely on Blob URLs and download attributes

## File References

- [index.html](index.html): Complete application - modify CSS in `<style>`, JS in `<script>`, HTML structure in `<body>`</content>
  <parameter name="filePath">c:\Users\Rodrigo\Documents\GitHub\Site-onlines\.github\copilot-instructions.md
