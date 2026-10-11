# Project Rules & Guidelines

## Prompt Logging Requirement
- **Mandatory Action**: Whenever any user prompt or request is received in this project, immediately persist the exact user prompt content to the `_\logs` folder.
- **Naming Convention**: The file name must strictly follow the format `YYYYMMDD_HHMMSS.txt` using the timestamp when the prompt was received (in local time).
- **Location**: `_\logs\` relative to the workspace root (`c:\Users\user\icon-ba\_\logs`).
- **Timing**: Ensure the prompt is saved at the start of processing each user request.
