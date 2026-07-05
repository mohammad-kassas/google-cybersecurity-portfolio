# File Permissions in Linux

**Analyst:** Mohammad
**Environment:** Linux Bash shell (Debian-based distribution)
**Working directory:** /home/researcher2/projects

---

## Project Description

As a security professional working with a research team, part of my role is to ensure that users are authorized with appropriate permissions on the file system. In this project, I examined existing permissions on files and directories in the `/home/researcher2/projects` directory, identified any permissions that did not align with the organization's authorization policy, and used Linux commands to modify them accordingly. This work directly applies the principle of least privilege — ensuring users have only the access they actually need, and no more.

---

## Check File and Directory Details

To check all permissions in the `projects` directory, including hidden files, I used:

```bash
ls -la
```

The `-l` flag displays permissions, ownership, file size, and modification time in long format. The `-a` flag includes hidden files (those beginning with a `.`). Combining them as `-la` gives a complete picture of all file and directory permissions, including any hidden entries.

**Output:**

```
total 32
drwxr-xr-x 3 researcher2 research_team 4096 Jul  5 10:09 .
drwxr-xr-x 3 researcher2 research_team 4096 Jul  5 10:09 ..
-rw--w---- 1 researcher2 research_team   46 Jul  5 10:09 .project_x.txt
drwx--x--- 2 researcher2 research_team 4096 Jul  5 10:09 drafts
-rw-rw-rw- 1 researcher2 research_team   46 Jul  5 10:09 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Jul  5 10:09 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Jul  5 10:09 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Jul  5 10:09 project_t.txt
```

The hidden file `.project_x.txt` is visible here because of the `-a` flag — it would not appear with a plain `ls` or `ls -l`.

The group that owns all files in the `projects` directory is **research_team**.

---

## Describe the Permissions String

Using `project_k.txt` as the example: `-rw-rw-rw-`

| Position | Character | Meaning |
|---|---|---|
| 1st | `-` | Regular file (not a directory; `d` would indicate a directory) |
| 2nd | `r` | User (owner) has **read** permission |
| 3rd | `w` | User (owner) has **write** permission |
| 4th | `-` | User (owner) does **not** have execute permission |
| 5th | `r` | Group has **read** permission |
| 6th | `w` | Group has **write** permission |
| 7th | `-` | Group does **not** have execute permission |
| 8th | `r` | Other (all other users) has **read** permission |
| 9th | `w` | Other has **write** permission — **this is the problem** |
| 10th | `-` | Other does **not** have execute permission |

The `w` in position 9 means any user on the system can modify this file, which violates the organization's policy.

---

## Change File Permissions

The organization does not allow the `other` owner type to have write access to any files. Checking the output above, `project_k.txt` had permissions `-rw-rw-rw-`, meaning `other` had write access — the only file in the directory with this issue.

**Command used:**

```bash
chmod o-w project_k.txt
```

`o` targets the `other` owner type, `-` removes the specified permission, and `w` specifies write permission. This removes write access from `other` while leaving all other permissions unchanged.

**Verification:**

```bash
ls -l project_k.txt
```

Result: `-rw-rw-r--` — write permission for `other` has been removed, and `other` now has read-only access.

Additionally, `project_m.txt` had permissions `-rw-r-----`, meaning the group had read access when it should have none. This was fixed with:

```bash
chmod g-r project_m.txt
```

Result: `-rw-------` — only the user (researcher2) retains read and write access.

---

## Change File Permissions on a Hidden File

The hidden file `.project_x.txt` is an archived file. It should not be writable by anyone, but both the user and group should retain read access.

Checking its permissions from the `ls -la` output: `-rw--w----`
- User has read and write — write should be removed
- Group has write only — write should be removed, read should be added
- Other has no permissions — correct, no change needed

**Command used:**

```bash
chmod u-w,g-w,g+r .project_x.txt
```

This single command performs three operations simultaneously:
- `u-w` — removes write from the user
- `g-w` — removes write from the group
- `g+r` — adds read to the group

Note: multiple permission changes are separated by commas with no spaces between them. Hidden files must be referenced with their leading period (`.project_x.txt`), otherwise the shell won't find the file.

**Result:** `-r--r-----` — both user and group can read, nobody can write.

---

## Change Directory Permissions

Only `researcher2` should be able to access the `drafts` directory and its contents, meaning only `researcher2` should have execute permission on it.

Checking `drafts` from `ls -l`:

```
drwx--x--- 2 researcher2 research_team 4096 Jul  5 10:09 drafts
```

Permissions: `drwx--x---`
- User (researcher2): read, write, execute ✅
- Group (research_team): execute only — **this should be removed**
- Other: no permissions ✅

The group's execute permission on a directory means they can enter it and access its contents, which violates the requirement that only `researcher2` should have this access.

**Command used:**

```bash
chmod g-x drafts
```

`g` targets the group, `-` removes the permission, `x` specifies execute. After this command, the group can no longer enter the `drafts` directory or access its contents.

**Result:** `drwx------` — only `researcher2` retains full access to `drafts`.

---

## Summary

In this project, I used Linux Bash commands to examine and manage file and directory permissions for the `researcher2` user's project files, applying the principle of least privilege throughout. Using `ls -la`, I identified four permission violations: `other` had write access to `project_k.txt`; `group` had read access to the restricted `project_m.txt`; the hidden archived file `.project_x.txt` had incorrect write permissions for both user and group; and the `drafts` directory allowed the group to execute (enter), which was not authorized. I used `chmod` to correct each violation, removing unauthorized access while preserving the permissions that legitimate users actually need.
