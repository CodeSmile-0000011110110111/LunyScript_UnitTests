# Execution Plan

## 1. Analysis & Preparation
- [X] Identify unused `Timer_*_LunyScript` classes in `CoroutineTimerTests.cs`.
- [X] Determine expected behavior and verification steps (frames to simulate, variables to check).

## 2. Implementation
- [X] Add `Timer_AutoStarts` test method.
- [X] Add `Timer_StartsStopped_StartsLater` test method.
- [X] Add `Timer_StartsPaused_ResumeLater` test method.
- [X] Add `Timer_PausedLater_ResumeLater` test method.
- [X] Add `Timer_LowerTimeScale_TakesLonger` test method.
- [X] Add `Counter_AutoStarts` test method in `CoroutineCounterTests.cs`.

## 3. Verification
- [X] Run all tests in `LunyScript-Test`.
- [X] Confirm the new tests run and report failures where implementation is missing/broken.
