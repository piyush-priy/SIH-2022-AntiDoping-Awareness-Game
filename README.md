# SIH 2022 — Anti‑Doping Awareness Game (Unreal Engine 4.27)

An educational, gamified experience built for the Smart India Hackathon 2022 problem statement “Gamifying Anti‑Doping Awareness.”

Set in a stylized boxing environment, the game turns key anti‑doping concepts into interactive moments: you’ll move, block, and strike in short bouts; make choices when tempted by unfair shortcuts; and answer quick quizzes that convert rules and consequences into memorable decisions. Your actions culminate in a post‑match reflection screen that classifies your path (“No Doped”, “Slight Doped”, or “Doped”) and reinforces fair‑play principles.

> Engine: Unreal Engine 4.27 • Target: Windows • Project file: `boxing.uproject`

## Game overview

- Core loop
  1) Start at the Main Menu (`Levels/Main_Menu_Level`).
  2) Pick a path from the selection hub (`Levels/SelectGame_Level`) into a boxing scenario and/or quiz.
  3) Play short combat sequences using simple controls (move, look, punch, power punch, block; see Controls below).
  4) Encounter decision prompts and quiz interludes (`StarterContent_Quiz/Maps/Quiz_Map`) tied to anti‑doping awareness.
  5) Complete the session to see a summary and learning feedback (`Levels/After_Quiz`, `AfterGame/After_Game`).

- Learning goals (through play)
  - Understand that short‑term “advantages” from unfair choices carry long‑term risks and penalties.
  - Recognize clean‑sport best practices and make the right call under pressure.
  - Retain knowledge via lightweight question prompts and immediate feedback.

- Scenarios and flow
  - Main Menu → Game Select → Boxing and/or Quiz map(s) → After‑Quiz → After‑Game outcome
  - Outcome widgets/screens include: `No_Doped`, `Slight_Doped`, `Doped`, and `DopingScreen` for clear, actionable feedback.

- Presentation and interaction
  - Boxing‑themed movement/combat uses third‑person inputs for quick onboarding.
  - UI/Widgets highlight choices and results without interrupting flow.
  - Designed for short sessions, quick restarts, and repeatable learning.

## What’s inside

- Main menu and game flow
  - Default startup map: `Content/Levels/Main_Menu_Level.umap`
  - Level flow includes: `SelectGame_Level`, `StarterContent_Quiz/Maps/Quiz_Map`, `Levels/After_Quiz`, and `AfterGame/After_Game`
- Core gameplay and learning
  - Boxing movement and combat (WASD + mouse; punch, power punch, block)
  - Quiz/decision screens that convey anti‑doping knowledge during progression
  - Post‑game feedback screens (e.g., doped/no‑doped outcomes) and infographics/widgets
- Content highlights (folders)
  - `Content/Levels/` — Main menu and selection/flow maps
  - `Content/StarterContent_Quiz/` — Quiz maps and assets
  - `Content/AfterGame/` — After‑match feedback UIs (`DopingScreen`, `Doped_Widget`, etc.)
  - `Content/Animations` and `Content/Animations_Boxing` — Character and enemy animation blueprints and blend spaces
  - `Content/Final_Widgets`, `Content/HUD`, `Content/Main_Menu`, `Content/widget` — UI and menu widgets

## Repository layout (top‑level)

- `boxing.uproject` — UE project descriptor (UE 4.27). Includes MultiUserClient plugin and `WindowsNoEditor` target.
- `Config/` — Project settings
  - `DefaultEngine.ini` — Game default map, startup map, default GameMode
  - `DefaultGame.ini` — Project name and packaging settings, maps to cook
  - `DefaultInput.ini` — Keybindings for movement, combat, pause, respawn
- `Content/` — All game assets (maps, blueprints, widgets, animations, media)
- `Binaries/`, `Intermediate/`, `DerivedDataCache/`, `Saved/` — Generated/build artifacts (usually ignored in Git)

## Prerequisites

- Windows 10/11 64‑bit
- Unreal Engine 4.27.x installed (Epic Games Launcher)
- Disk space: 25–40 GB recommended for source + derived data on first open
- Optional for development builds:
  - Visual Studio 2019/2022 with Desktop development with C++ (for compiling code projects; this project appears Blueprint‑driven but VS helps with build tools)
- Recommended for cloning from GitHub:
  - Git LFS (for large binary assets like `.uasset`, `.umap`, audio, etc.)

## Getting set up

### 1) Clone the repository

```powershell
# Install Git LFS once per machine (if not already)
winget install Git.Git -e ; winget install GitHub.GitLFS -e
git lfs install

# Clone
git clone https://github.com/<your-org-or-user>/SIH-2022-AntiDoping-Awareness-Game.git
cd SIH-2022-AntiDoping-Awareness-Game
```

If you see files that contain only small text pointers instead of binary data (e.g., for `.uasset`/`.umap`), run `git lfs install` and re‑pull.

### 2) Open in the Unreal Editor

- Double‑click `boxing.uproject`, or open UE 4.27 and browse to the project.
- UE will prompt to build shaders and compile derived data on first launch; let it finish.
- The default startup map is the main menu: `Content/Levels/Main_Menu_Level.umap`.

### 3) Play in editor (PIE)

- Press Play in the toolbar to start.
- Use the controls listed below. Follow on‑screen prompts for quiz/decisions.

## Controls (from `Config/DefaultInput.ini`)

- Movement: `W`/`A`/`S`/`D`
- Look: Mouse (Move)
- Jump: `Space`
- Punch: Left Mouse Button
- Power Punch: Right Mouse Button
- Block: `Left Shift`
- Pause: `Esc` or `P`
- Respawn: `R`
- Fullscreen toggle: `Alt+Enter` or `F11`

## Packaging a Windows build

These settings are already configured in `Config/DefaultGame.ini` (Shipping, Pak/Oodle compression, selected maps to cook). To package:

1. In UE Editor: `File` → `Package Project` → `Windows (64‑bit)`.
2. Choose an output folder. UE will cook the maps and create a `WindowsNoEditor` build.
3. The packaged game folder will contain an executable (e.g., `WindowsNoEditor\<ProjectName>.exe`). Share the whole folder to run on another PC.

Notes:
- Maps flagged to cook include: `Levels/Main_Menu_Level`, `Levels/SelectGame_Level`, `Levels/After_Quiz`, `Start_Finish/NewMap`, `StarterContent_Quiz/Maps/Quiz_Map`, and `AfterGame/After_Game`.
- Shipping configuration is enabled; crash reporter is disabled by default.

## Running an already packaged build

If the repository includes a packaged build (e.g., under `Build/WindowsNoEditor/` or `Saved/StagedBuilds/WindowsNoEditor/`):

- Navigate to that directory and run the `.exe` file. No editor installation is required.
- If DLL errors occur, ensure Microsoft VC++ Redistributables are installed (UE can package prerequisites, or install via Windows Update/Visual Studio installer).

## Troubleshooting

- Engine version mismatch
  - Project targets UE `4.27`. If you open in another version, UE may ask to convert. Prefer installing UE 4.27 to avoid migration risk.
- Missing/placeholder assets after clone
  - Make sure Git LFS is installed and active. Run `git lfs install` and then `git pull` again.
- Long initial load or compilation
  - First open will build shaders and derived data. Subsequent loads are much faster.
- “Map not found” or boots to a blank level
  - Check `Edit → Project Settings → Maps & Modes`. `Game Default Map` should be `Levels/Main_Menu_Level` as set in `DefaultEngine.ini`.
- Controls don’t work as expected
  - Verify input bindings in `Config/DefaultInput.ini` or within the editor under Project Settings → Input.

## Contributing

- Use feature branches and pull requests.
- Large binary assets should be tracked with Git LFS (e.g., `*.uasset`, `*.umap`, `*.wav`, `*.fbx`).
- Prefer keeping `Binaries/`, `DerivedDataCache/`, `Intermediate/`, and `Saved/` out of source control.

## License and acknowledgements

- Built for Smart India Hackathon 2022 — Problem Statement: Gamifying Anti‑Doping Awareness.
- License: Add your preferred license here (e.g., MIT/Apache‑2.0/Proprietary). If unsure, start with an open‑source license compatible with game assets you include.

---

### Quick reference (settings pulled from project files)

- UE project: `boxing.uproject`
- Engine: 4.27
- Game default map: `/Game/Levels/Main_Menu_Level`
- Editor startup map: `/Game/StarterContent/Maps/Minimal_Default`
- Default GameMode: `/Game/Main_Menu/Main_Menu_GameMode`
- Key maps cooked for Windows builds: Main Menu, Select Game, After Quiz, Start/Finish, Quiz_Map, After_Game
