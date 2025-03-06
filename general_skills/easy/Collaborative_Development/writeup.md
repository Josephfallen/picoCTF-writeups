# **picoCTF 2024 - Collaborative Development Writeup**  

## **Challenge Description**  
We are given a compressed file (`challenge.zip`) that contains a Git repository. Inside, multiple branches hold different **parts of a script**, and our goal is to **reconstruct the full script** by combining those parts.  

Branches provided:  
- `main`  
- `feature/part-1`  
- `feature/part-2`  
- `feature/part-3`  

The flag is likely revealed once the script is fully assembled and executed.  

---

## **Step 1: Download and Extract the Repository**  
Since the challenge does not provide direct Git access, we download and extract the files manually.  

```bash
wget https://artifacts.picoctf.net/c_titan/70/challenge.zip
unzip challenge.zip -d challenge
cd challenge
```

To confirm it’s a Git repository, check for the `.git` directory:  

```bash
ls -la
```

If `.git` exists, we can proceed with Git commands. If not, we may need to initialize it (`git init`), but that’s unlikely for this challenge.  

---

## **Step 2: List Available Branches**  
Since we can’t use `git clone`, we manually inspect the repository’s branches:  

```bash
git branch -a
```

This should list:  
```
* main
  feature/part-1
  feature/part-2
  feature/part-3
```

We switch to each branch and examine the contents.  

---

## **Step 3: Extracting Parts of the Script**  
We start by switching to `feature/part-1` and checking the files.  

```bash
git checkout feature/part-1
ls
cat <script_filename>
```

We repeat this for the remaining branches:  

```bash
git checkout feature/part-2
cat <script_filename>

git checkout feature/part-3
cat <script_filename>
```

Each part contains a **fragment of the final script**, which we will piece together.  

---

## **Step 4: Merging the Parts**  
Now, we reconstruct the script by combining all the parts.  

1. Open a new file:  

   ```bash
   nano full_script.py
   ```

2. Copy each extracted part in order. The correct order is usually **part-1 → part-2 → part-3**.  
   
3. Save and exit (`CTRL + X`, then `Y`, then `ENTER`).  

---

## **Step 5: Running the Script**  
After merging the parts, we execute the script to reveal the flag.  

```bash
python3 full_script.py
```


---

## **Step 6: Capture the Flag**  
Once executed, the script should print the flag in the format:  

```
picoCTF{...}
```

Copy and submit the flag to **picoCTF**! 🎉  

---

## **Conclusion**  
This challenge teaches us how to:  
✅ Extract data from Git branches  
✅ Compare and merge code manually  
✅ Reconstruct a full script from parts  

This process mirrors **real-world software development**, where code is split across multiple branches and must be merged correctly.  
