# Wong Chun Cheung (Alex)

**English** — Computer Science student at City University of Hong Kong. I like building
systems end to end: the firmware, the recognition pipeline, the data layer, and the
tooling around them.

**中文** — 香港城市大學電腦科學系學生。我喜歡把系統由頭到尾自己完成：韌體、辨識管線、
資料層，以及圍繞它們的工具。

<!-- TODO: 開設 LinkedIn 後，在這裡加入一行連結。
     TODO: once LinkedIn exists, add a link line here. -->

---

## Featured projects · 精選專案

### 1 · FixIt — an agentic C++ repair loop · 代理式 C++ 修復迴圈

`C++20` · `CMake` · `Catch2` · `tree-sitter` · `LLM` · `GitHub Actions` · individual project

**English** — The bottleneck in agentic code repair is rarely the model; it is that the
patch does not apply. FixIt closes the loop `compile → locate → LLM patch → fuzzy apply →
re-verify`, and its patch engine is built for the diff a model *actually* produces:
drifted line numbers, missing context, and whitespace that does not quite match.

**中文** — 代理式程式修復的瓶頸通常不在模型，而在 **patch 套用不上**。FixIt 把
`compile → locate → LLM patch → fuzzy apply → re-verify` 串成閉環，其 patch 引擎專為
模型**真正**產出的 diff 而設：行號漂移、context 缺失、空白不完全相符。

**Inside · 技術重點**

- **Fuzzy patch engine** — every candidate position is scored
  (`exact` / `fuzzy` / `mismatch`, normalised so a perfect hunk is `1.00`), searched
  through a window ladder `±0 → ±1 → ±2 → ±5 → ±10 → ±50 → global`, and gated at
  `score ≥ 0.80` with at least one exact line.
- **Structured failure that feeds the loop** — a refused hunk returns the score, the
  closest match, the exact line that differed, and a suggested re-read, so the model can
  act on it instead of guessing again.
- **The compiler is the only ground truth** — a model that answers `FINAL` still triggers
  a compile; `success` is set only by a clean exit.

**Measured · 實測** — 200 trials per cell, with all four impairments present in every
cell: **100%** apply rate up to **±20 lines** of drift, **99%** at ±50.

**Verification · 驗證** — CI runs on Ubuntu (gcc-12) and macOS (clang): configure, build,
`ctest`, then a demo smoke test that also asserts the mock *must not* fix the case it is
not supposed to fix — and that the working tree is left byte-identical.

→ [Repository](https://github.com/wong060404/FixIt)

### 2 · Living Hour Counting System — 居住時數統計系統 · ESP32 + OpenCV

`ESP32-CAM` · `MicroPython` · `Python` · `OpenCV (LBPH)` · `MOSSE tracking` · `SQLite` · team of 5 — I was project leader & lead developer

**English** — A face-recognition door that logs who entered, when, and for how long, then
reports the flats falling below Hong Kong's 150-hour monthly occupancy rule. The point is
not the lock: it is turning a stream of entry events into an auditable monthly figure.

**中文** — 一套人臉辨識門禁系統：記錄誰在甚麼時候進出、停留多久，然後列出每月居住時數
低於香港 150 小時規定的單位。重點不在門鎖，而在於把一連串進出事件變成可稽核的每月數字。

**My part · 我負責的部分**

- Designed the OpenCV pipeline end to end: `capture.py`, `process_and_train.py`, and
  `track_and_recognize.py`, including the MOSSE tracker and the multi-frame voting
  mechanism that decides when to unlock.
- Built the hardware–software integration: turned the ESP32 into a local web server and
  wired the unlock call into the recognition loop, with failure handling that keeps the
  video loop alive when the relay node is unreachable.
- Consolidated the scripts behind `Control_System.py`, and led testing and debugging.

**Engineering notes · 工程取捨** — The repository ships bilingual documentation, an
explicit privacy and data-handling section (the system processes biometric data under the
PDPO), and a section listing the prototype's honest limitations — tailgating inverting the
entry/leave state, no liveness detection, and LBPH's sensitivity to lighting.

→ [Repository](https://github.com/wong060404/Living-Hour-Counting-System-ESP32)

### 3 · Vocab Master — an Android vocabulary trainer · Android 單字訓練器

`Java` · `Android SDK` · `Room (SQLite)` · `Lottie` · individual project

**English** — A trainer built around a practical observation from tutoring: fixed word
lists cannot match the vocabulary a student's quiz will actually cover next week. Users
build their own groups, study them, then prove recall through Tap-to-Match and Spelling
modes. Offline-first: no account, no network.

**中文** — 這套工具的出發點來自補習時的觀察：固定的字庫無法配合學生下週測驗真正要考的
範圍。使用者自行建立字組、研讀，再透過「配對」與「拼寫」兩種模式證明自己真的記得。
離線優先：無需帳號、無需網絡。

→ [Repository](https://github.com/wong060404/vocab-master)

---

## Toolbox · 技術棧

| | |
|---|---|
| **Languages** | C++20 · Python · Java · Bash / PowerShell |
| **Systems & tooling** | CMake · Catch2 · clang / GCC · GitHub Actions · git · tree-sitter |
| **Computer vision & ML** | OpenCV (LBPH, Haar cascades, MOSSE tracking) · LLM API integration |
| **Embedded** | ESP32 / ESP32-CAM · MicroPython · GPIO & relay control |
| **Data & applications** | SQLite · Room · Android SDK |
| **Working habits** | bilingual documentation · CI on two compilers · recorded, reproducible demos |

## Background · 背景

**English** — Currently studying Computer Science at City University of Hong Kong.
Previously completed an Associate of Engineering at HKU SPACE Community College, where my
final-year project was the ESP32 occupancy system above.

**中文** — 現正於香港城市大學修讀電腦科學。此前於 HKU SPACE Community College 完成工程學副學士，
畢業專題即上方的 ESP32 居住時數系統。
