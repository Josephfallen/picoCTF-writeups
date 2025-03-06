# Commitment Issues Writeup

## Challenge Description
The challenge, "Commitment Issues," hints at something related to commits, likely in a Git repository. The goal is to locate a flag hidden in a previous commit.

## Solution

1. **Downloading the Challenge Files**
   Start by downloading the challenge archive using `wget`:
   ```sh
   wget https://artifacts.picoctf.net/c_titan/138/challenge.zip
   ```
   Extract the contents:
   ```sh
   unzip challenge.zip
   cd challenge
   ```

2. **Checking Commit History**
   If the directory contains a Git repository, inspect the commit history:
   ```sh
   git log --oneline
   ```
   This displays a compact history of commits, showing commit hashes and messages.

3. **Examining Older Commits**
   If the flag was removed in a later commit, check an earlier version of the repository:
   ```sh
   git checkout <commit_hash>
   ```
   Replace `<commit_hash>` with a hash from the commit log.

4. **Finding the Flag**
   Once inside an older commit, search for the flag:
   ```sh
   grep -r "flag" .
   ```
   If the flag follows a specific format, such as `CTF{}`, adjust the search:
   ```sh
   grep -r "picoCTF{" .
   ```
   You can also check specific files using:
   ```sh
   git show <commit_hash>:<file_path>
   ```

5. **Restoring to the Latest Commit**
   After retrieving the flag, return to the latest commit:
   ```sh
   git checkout main
   ```

## Conclusion
By analyzing past commits, we were able to locate the flag hidden in a previous version of the repository. This challenge reinforces the importance of commit history and version control awareness in security challenges.
