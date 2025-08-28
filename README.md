# `trash` and `restore` Scripts

This repository contains a pair of scripts for safer file management. The `trash` script acts as a safe delete, moving files to a trash folder instead of permanently deleting them. The `restore` script allows you to easily retrieve those files.

## How the Scripts Work

### The `trash` Script

The `trash` script is a safer alternative to the standard `rm` command. When you use it, it doesn't permanently delete files. Instead, it **moves** them to a dedicated trash directory located at `/tmp/trash/`. This process includes a few key steps:

* **Creates a trash directory:** If `/tmp/trash/` doesn't exist, the script will automatically create it.

* **Adds a timestamp:** To prevent file name conflicts, each file is renamed with a unique timestamp upon deletion. This means you can "trash" multiple files with the same original name without them overwriting each other.

* **Logs the action:** The script keeps a record of every file deletion in a log file at `/tmp/trash/trash.log`, noting the original file path and the new location.

### The `restore` Script

The `restore` script is designed to bring your files back from the trash. It works by:

* **Reading the log:** It scans the `trash.log` file for the most recent entry that matches the file you want to restore.

* **Moving the file:** It moves the timestamped file from the `/tmp/trash/` directory back to its original location.

* **Handling conflicts:** If a file with the same name already exists at the destination, the `restore` script will intelligently rename the restored file by adding a `.restored` suffix to avoid overwriting anything.

## Handling Edge Cases

These scripts are designed to be robust and handle common issues:

* **Missing files:** If you try to delete a file that doesn't exist, the script won't crash. It will display a clear error message.

* **Directory deletion:** Just like the standard `rm` command, the `trash` script requires the **`-r`** flag to recursively delete an entire directory and its contents.

* **Restoring to an existing location:** If you try to restore a file to a directory where a file with the same name already exists, the `restore` script will automatically rename the restored file to prevent accidental overwriting.

## Examples

Here are some common use cases for the scripts:

### Trashing a File

```bash
# Move a single file to the trash
$ trash test1.txt
```

### Trashing a Directory

```bash
# Move a directory and all of its contents to the trash
# The `-r` flag is required for recursive deletion
$ trash -r testfolder
```

### Restoring a File

```bash
# Move a single file to the trash
$ trash test1.txt
```

### Restoring a Directory

```bash
# Move a single file to the trash
$ trash testfolder
```
