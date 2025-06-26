- We use the `sys` module in Python, which provides various functions and variables that are used to manipulate different parts of the **python runtime environment**

```python
import sys

  

def error_message_details(error, error_detail):

    _, _, exc_tb = error_detail.exc_info()  # gets the traceback info

    file_name = exc_tb.tb_frame.f_code.co_filename

    error_message = "Error has occurred in python script name [{0}] line number [{1}] error message [{2}]".format(

        file_name,

        exc_tb.tb_lineno,

        str(error)

    )

    return error_message

  

class CustomException(Exception):

    def __init__(self, error_message, error_detail):

        super().__init__(error_message)

        self.error_message = error_message_details(error_message, error_detail=error_detail)

    def __str__(self):

        return self.error_message
```
## 📜 Full Picture: What does this code do?

You're making a **custom exception class** that gives you **detailed, user-friendly error messages** including:

- Filename 🗂️
    
- Line number 🔢
    
- Error message ⚠️
    

Basically turning boring errors into Sherlock Holmes-level clues 🔍🧠

---

## 🧠 Code Breakdown (Section by Section):

### 🧩 `import sys`

You're importing Python’s `sys` module to get juicy low-level info about exceptions.

---

### 🔧 `error_message_details()`

This function extracts detailed traceback info and formats a custom message 💌


```python
def error_message_details(error, error_detail):
```

- `error`: the actual error object (like `ZeroDivisionError`)
    
- `error_detail`: typically you pass in `sys`, so you can access `sys.exc_info()`

``` python
_, _, exc_tb = error_detail.exc_info()
```

- `exc_info()` returns a tuple: `(exception_type, exception_object, traceback_obj)`
    
- You only want `exc_tb`, the traceback object 🧾

```python
file_name = exc_tb.tb_frame.f_code.co_filename
```

- Get the **filename** where the error happened 🤓  
    (like `main.py` or `data_ingestion.py`)
    
```python
exc_tb.tb_lineno
```

- Grabs the **exact line number** where your code broke 😵
    
```python 
error_message = "Error has occurred in python script name [{0}] line number [{1}] error message [{2}]".format(...)
```

- This is the final spicy error string you’ll see in logs 🌶️
    

---

### 💥 `class CustomException(Exception):`

You’re creating your own error class by inheriting from Python’s built-in `Exception` class 😤  
Like a final boss override 💀


```python
def __init__(self, error_message, error_detail):
```

- This runs when you raise the exception
    
- `error_message`: what you pass in
    
- `error_detail`: `sys`, so we can grab traceback info again


```python
super().__init__(error_message)
```

- Calls parent class constructor (`Exception`) to keep it functional
    
```python
self.error_message = error_message_details(error_message, error_detail=error_detail)
```

- Calls the helper function to build that **juicy message**
    

---

### 🗣️ `def __str__(self):`

When you print the exception (or log it), this is what gets shown.

```python
return self.error_message
```

So the output will be like:

```
Error has occurred in python script name [my_script.py] line number [42] error message [division by zero]`
```

---

## 🧪 How it Works in Action:


```python
try:     x = 1 / 0  # 🔥 This breaks! except Exception as e:     raise CustomException(e, sys)
```

Instead of:

```vbnet
ZeroDivisionError: division by zero
```
You’ll get:

```txt
Error has occurred in python script name [main.py] line number [2] error message [division by zero]
```
_Much better for debugging your spicy ML pipelines or backend logic_ 😤🍜

---

## 🌈 Final Thoughts:

✅ Super useful for logging  
✅ Makes error tracing 100x easier  
✅ Can be extended to log to a file, DB, or even send alerts 🚨