# File Permissions in Linux

## Overview
This project is a Linux file permissions management exercise completed as part of the Google Cybersecurity Certificate (Course 5: Tools of the Trade — Linux and SQL). Using Linux Bash commands, I examined file and directory permissions, identified violations of the principle of least privilege, and corrected them using `chmod`.

## Scenario
As a security professional on a research team, I was tasked with auditing permissions on the `/home/researcher2/projects` directory. I identified files and directories with incorrect permissions and modified them to ensure only authorized users had the appropriate level of access.

## Skills Demonstrated
- Reading and interpreting the 10-character Linux permission string (`drwxrwxrwx`)
- Using `ls -l` and `ls -la` to inspect permissions, including on hidden files
- Using `chmod` with `u`, `g`, `o` and `+`, `-`, `=` operators to modify permissions precisely
- Applying multi-operation `chmod` commands in a single pass (e.g., `u-w,g-w,g+r`)
- Working with hidden files (dot-prefixed filenames) in the Linux file system
- Applying the principle of least privilege to real file permission scenarios

## Files
- [`file-permissions-in-linux.md`](./file-permissions-in-linux.md) — full written portfolio document
- [`file-permissions-in-linux.pdf`](./file-permissions-in-linux.pdf) — PDF version

## Key Finding
Four permission violations were identified and corrected across the `projects` directory: unauthorized write access by `other` on `project_k.txt`; unauthorized group read access on the restricted `project_m.txt`; incorrect write permissions on the archived hidden file `.project_x.txt`; and unauthorized group execute access on the `drafts` directory. All were corrected using targeted `chmod` commands without affecting legitimate user permissions.
