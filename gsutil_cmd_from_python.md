## How to use `gsutil` commands in python script to take backup of source file before processing ?

### Shortened Python Script Using a Single String for the Command:

```python
import subprocess

def backup_file(source, backup):
    try:
        # Run gsutil command directly as a string
        subprocess.run(f'gsutil cp {source} {backup}', check=True, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE, text=True)
        print(f"Backup from {source} to {backup} successful.")
    except subprocess.CalledProcessError as e:
        print(f"Backup failed: {e.stderr}")

# Example usage
backup_file('gs://your-bucket-name/file-to-backup.txt', 'gs://your-bucket-name/backup/file-to-backup.txt')
```

### Explanation:
1. **String command**: The command is passed as a single string (`f'gsutil cp {source} {backup}'`), where `source` and `backup` are dynamically inserted.
2. **`shell=True`**: This tells `subprocess.run()` to run the command in a shell, which allows you to use string commands (like `gsutil cp`).
3. **Error handling**: If `gsutil` fails, it will raise a `CalledProcessError`, and the error message will be printed.

### Notes:
- **Security Consideration**: When using `shell=True`, ensure that the inputs (`source` and `backup`) are properly sanitized, as it can open up security risks (e.g., shell injection) if the inputs come from untrusted sources. In your case, since the inputs are file paths, it should be safe, but always keep security in mind when using `shell=True`.
- **`stdout` and `stderr`**: These are captured to handle any outputs or errors, but they're not used here in the final print statements. You can add more logic to handle the captured output if needed.

This is the shortest and most direct way to run a `gsutil cp` command from Python using `subprocess.run()`.
