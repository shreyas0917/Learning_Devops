# Day 38 – YAML Basics

## Objective

Today I learned the fundamentals of YAML, which is the configuration language used in most CI/CD tools like GitHub Actions, GitLab CI, Azure DevOps, Kubernetes, Docker Compose, and Ansible.

---

# Task 1: Key-Value Pairs

### person.yml

```yaml
---
name: Shreyas Wani
role: DevOps Engineer
experience_years: 0
learning: true
```

### Verification

```bash
cat person.yml
```

Output:

```yaml
---
name: Shreyas Wani
role: DevOps Engineer
experience_years: 0
learning: true
```

---

# Task 2: Lists

Updated **person.yml**

```yaml
---
name: Shreyas Wani
role: DevOps Engineer
experience_years: 0
learning: true

tools:
  - Linux
  - Git
  - Docker
  - Kubernetes
  - GitHub Actions

hobbies: [Gym, Reading, Coding]
```

### Two Ways to Write Lists in YAML

### Block Style

```yaml
tools:
  - Docker
  - Kubernetes
  - Terraform
```

### Inline Style

```yaml
tools: [Docker, Kubernetes, Terraform]
```

---

# Task 3: Nested Objects

### server.yml

```yaml
---
server:
  name: production-server
  ip: 192.168.1.10
  port: 8080

database:
  host: localhost
  name: devopsdb
  credentials:
    user: admin
    password: password123
```

### Verification

If a **tab** is used instead of spaces, YAML validation fails because YAML only supports spaces for indentation.

Example error:

```text
found character '\t' that cannot start any token
```

---

# Task 4: Multi-line Strings

Updated **server.yml**

```yaml
---
server:
  name: production-server
  ip: 192.168.1.10
  port: 8080

database:
  host: localhost
  name: devopsdb
  credentials:
    user: admin
    password: password123

startup_script_literal: |
  #!/bin/bash
  echo "Starting application..."
  docker compose up -d
  echo "Application Started"

startup_script_folded: >
  This startup script installs dependencies,
  starts the Docker containers,
  and verifies that the application
  is running successfully.
```

### Difference Between `|` and `>`

| Symbol | Purpose |
|---------|---------|
| `|` | Preserves line breaks exactly as written. Useful for shell scripts, configuration files, certificates, or multi-line commands. |
| `>` | Folds multiple lines into a single line. Useful for long descriptions, documentation, or messages. |

---

# Task 5: Validate YAML

## Install yamllint

Ubuntu:

```bash
sudo apt update
sudo apt install yamllint -y
```

Verify installation:

```bash
yamllint --version
```

Validate both YAML files:

```bash
yamllint person.yml
```

```bash
yamllint server.yml
```

### Errors Encountered

While validating, I encountered the following issues:

- Missing document start (`---`)
- Trailing spaces
- Too many blank lines

Example:

```text
person.yml
  1:1 warning missing document start "---"
  3:20 error trailing spaces

server.yml
  1:1 warning missing document start "---"
  14:1 error too many blank lines
  19:29 error trailing spaces
```

### Fixes Applied Using Vim

I used **Vim** to correct the formatting issues.

Open the file:

```bash
vim person.yml
```

or

```bash
vim server.yml
```

Remove trailing spaces from the entire file:

```vim
:%s/\s\+$//g
```

Save and quit:

```vim
:wq
```

After fixing the formatting, validate again:

```bash
yamllint person.yml
yamllint server.yml
```

No output means the YAML files are valid.

---

# Task 6: Spot the Difference

### Correct

```yaml
name: devops
tools:
  - docker
  - kubernetes
```

### Broken

```yaml
name: devops
tools:
- docker
  - kubernetes
```

### What's Wrong?

The list items are not consistently indented under the `tools` key.

Correct indentation:

```yaml
tools:
  - docker
  - kubernetes
```

YAML is indentation-sensitive, so incorrect spacing changes the structure and may cause validation errors.

---

# What I Learned

1. YAML uses **spaces only**; tabs are not allowed.
2. Lists can be written in **block style** or **inline style**.
3. Multi-line strings use `|` (preserve newlines) and `>` (fold into one line).
4. `yamllint` is useful for detecting indentation, trailing spaces, and formatting issues.
5. Vim commands like `:%s/\s\+$//g` make it easy to remove trailing whitespace from an entire file.

---

# Repository Structure

```text
2026/
└── day-38/
    ├── person.yml
    ├── server.yml
    └── day-38-yaml.md
```

---

# Conclusion

Today I learned the fundamentals of YAML, including key-value pairs, lists, nested objects, multi-line strings, and indentation rules. I also learned how to validate YAML files using `yamllint` and fix common formatting issues such as trailing spaces, blank lines, and missing document markers using **Vim**. These skills are essential for working with GitHub Actions, Docker Compose, Kubernetes, Ansible, and other DevOps tools that rely on YAML configuration files.