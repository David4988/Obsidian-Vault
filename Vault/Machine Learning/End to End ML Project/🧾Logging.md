
This script configures a logging system that saves log messages to a **timestamped `.log` file** inside a `/logs/` directory.

---
```python
import logging

import os

  

from datetime import datetime

  

LOG_FILE = f"{datetime.now().strftime('%m_%d_%Y_%H_%M_%S')}.log"

log_path = os.path.join(os.getcwd(),"logs", LOG_FILE)

os.makedirs(log_path,exist_ok=True)

  

LOG_FILE_PATH = os.path.join(log_path,LOG_FILE)

  

logging.basicConfig(

    filename=LOG_FILE_PATH,

    format = "[ %(asctime)s] %(lineno)d %(name)s - %(levelname)s - %(message)s",

    level= logging.INFO

)
```
## 📦 Imports

```python
import logging import os from datetime import datetime
```

- `logging`: Built-in module to handle logs.
    
- `os`: Used to manage file paths and directories.
    
- `datetime`: Helps create a timestamp-based log filename.
    

---

## 🕒 Generate Timestamped Log File Name


```python
LOG_FILE = f"{datetime.now().strftime('%m_%d_%Y_%H_%M_%S')}.log"
```

- This creates a filename like `06_24_2025_23_45_12.log`.
    
- It uses the current date and time to uniquely name each log file.
    

---

## 🗂️ Create Logs Directory and File Path

```python
log_dir = os.path.join(os.getcwd(), "logs") os.makedirs(log_dir, exist_ok=True)  LOG_FILE_PATH = os.path.join(log_dir, LOG_FILE)
```

- `log_dir`: Constructs the full path to the `/logs/` directory in the current working directory.
    
- `os.makedirs(..., exist_ok=True)`: Creates the directory if it doesn't exist (avoids error if it already exists).
    
- `LOG_FILE_PATH`: Final full path to the log file.
    

---

## ⚙️ Configure Logging


```python
logging.basicConfig(
	filename=LOG_FILE_PATH,
	format="[ %(asctime)s] %(lineno)d %(name)s - %(levelname)s - %(message)s",         level=logging.INFO
)
```

### 🔍 Format Breakdown:

|Placeholder|Description|
|---|---|
|`%(asctime)s`|Timestamp of the log entry|
|`%(lineno)d`|Line number where the log was triggered|
|`%(name)s`|Logger's name (usually `root`)|
|`%(levelname)s`|Log level (e.g. INFO, ERROR)|
|`%(message)s`|The actual message logged|

- `level=logging.INFO`: Logs `INFO` and above (`WARNING`, `ERROR`, `CRITICAL`).
    

---

## 🧪 Sample Log Entry


```
[2025-06-24 23:45:12,123] 42 root - INFO - Training started [2025-06-24 23:45:14,101] 98 root - ERROR - Model crashed due to bad input
```

---

## ✅ Summary

- ✔️ Logs are saved to `logs/<timestamp>.log`
    
- ✔️ Each run generates a unique log file
    
- ✔️ Easy to trace logs by time, file, line number, and message