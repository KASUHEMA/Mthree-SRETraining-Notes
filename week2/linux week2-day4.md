# Regular Expressions (Regex) and Python

## Quantifiers in Regular Expressions (Regex) in Shell Scripting

Quantifiers in regex specify how many times a character or group of characters should appear in a string. They enable flexible pattern matching for efficient text processing.

### Common Quantifiers in Regex (Shell Scripting)

| Quantifier | Meaning | Example |
|------------|---------|---------|
| `*` (zero or more) | Matches 0 or more occurrences of the preceding character | `ba*` matches `b`, `ba`, `baa`, `baaa` |
| `+` (one or more) | Matches 1 or more occurrences (ERE only) | `ba+` matches `ba`, `baa`, `baaa` but not `b` |
| `?` (zero or one) | Matches 0 or 1 occurrence (ERE only) | `colou?r` matches `color` and `colour` |
| `{n}` | Matches exactly n occurrences (ERE only) | `a{3}` matches `aaa` |
| `{n,}` | Matches at least n occurrences (ERE only) | `a{2,}` matches `aa`, `aaa`, `aaaa`, etc. |
| `{n,m}` | Matches between n and m occurrences (ERE only) | `a{2,4}` matches `aa`, `aaa`, or `aaaa` |

### Usage in Shell Scripting

#### Using `grep` (ERE mode with `-E`)
```sh
echo "baaaa" | grep -E "ba{2,4}"
```
Matches `baa`, `baaa`, or `baaaa`.

#### Using `sed` (ERE mode with `-E`)
```sh
echo "color" | sed -E 's/colou?r/colour/'
```
Replaces `color` or `colour` with `colour`.

#### Using `awk`
```sh
echo "hello123" | awk '/hello[0-9]+/'
```
Matches `hello` followed by one or more digits.

---

## Escaping in Regular Expressions (Regex)

Escaping in regex means using a backslash (`\`) before a special character to treat it as a literal character.

- Without escaping: `.` matches any character.
- With escaping (`\.`): `\.` matches a literal dot (`.`).

---

## Difference Between Basic (BRE) and Extended Regular Expressions (ERE)

### 1. Basic Regular Expressions (BRE)
- Used by: `grep`, `sed`, `awk` (default mode)
- Special characters must be escaped to work as regex operators.

| Feature | BRE (Basic) | ERE (Extended) |
|---------|------------|---------------|
| `+` (One or more) | `\+` | `+` |
| `?` (Zero or one) | `\?` | `?` |
| `{}` (Quantifiers) | `\{n,m\}` | `{n,m}` |
| `()` (Grouping) | `\(pattern\)` | `(pattern)` |
| `|` (OR) | `N/A` | `a|b` |

### 2. Extended Regular Expressions (ERE)
- Used by: `grep -E`, `sed -E`, `awk`
- No need to escape special characters (`+`, `?`, `{}`, `()`, `|`).
- More powerful and readable.

---

## Choosing Between `grep`, `sed`, and `awk`

| Feature | `grep` | `sed` | `awk` |
|---------|--------|--------|------|
| Pattern Matching | ✅ Yes | ✅ Yes | ✅ Yes |
| Substitutions (`s///`) | ❌ No | ✅ Yes | ✅ Yes |
| Column/Field Processing | ❌ No | ❌ No | ✅ Yes |
| Mathematical Operations | ❌ No | ❌ No | ✅ Yes |
| If-Else Logic | ❌ No | ❌ No | ✅ Yes |
| Formatted Output | ❌ No | ❌ No | ✅ Yes |

### Which One Should You Use?

| Command | When to Use |
|---------|-------------|
| `grep` | Simple filtering, no extra processing needed. |
| `awk` | When you need numeric comparisons (e.g., filtering `70-99`). |
| `sed` | When extracting or modifying log lines. |

![image](https://github.com/user-attachments/assets/f45bb56a-c24d-4a83-ad66-251c2daa3657)


---

## Email Validation Using Regex

![image](https://github.com/user-attachments/assets/4d8205e8-2970-475b-8780-11e8309f3084)

---

## Installation of Python and Bazel

### Python Installation
```sh
sudo apt update
sudo apt upgrade -y
sudo apt install -y python3-pip python-venv
sudo apt install -y python3-pip
python --version
python3 --version
pip3 --version
sudo apt install -y python3
```
![image](https://github.com/user-attachments/assets/eeb158ec-466a-418e-9f0f-dd474451fe8c)

### Bazel Installation
```sh
sudo apt install -y apt-transport-https curl gnupg
curl -fsSL https://bazel.build/bazel-release.pub.gpg | sudo gpg --dearmor > bazel-archive-keyring.gpg
sudo mv bazel-archive-keyring.gpg /usr/share/keyrings/bazel-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/bazel-archive-keyring.gpg] https://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list
sudo apt update
sudo apt install -y bazel
bazel --version
```
![image](https://github.com/user-attachments/assets/c28d69d5-38bd-4890-ac48-c4b7b7b0f8f8)

### Node.js Installation
```sh
sudo apt install -y nodejs npm
sudo npm install -g @bazel/bazelisk
```
![image](https://github.com/user-attachments/assets/8f08c185-32d6-45d3-ae14-07e13eb5759b)

---

## Creating a Directory and Using It
```sh
mkdir ~/bazel-python-project
cd bazel-python-project/
echo "8.1.0" > .bazelversion
mkdir -p src/main/python
mkdir -p src/test/python
cd ..
ls -lrt
cd bazel-python-project/
```
![image](https://github.com/user-attachments/assets/3ed8b2f0-debe-4884-8056-433b7661dd60)

---

## Installed Ollama

1. Download Ollama from Google.
2. Open VS Code and install the "Continue" extension.
3. Verify installation:
```sh
ollama --version
ollama pull deepseek-r1:1.5b
ollama run deepseek-r1:1.5b
```
4. Configuration:
```json
{
  "title": "deepseekFree",
  "provider": "ollama",
  "model": "deepseek-r1:1.5b"
}
```

---

## Basic Python Program

```python
print("Hello, World!")
```
![image](https://github.com/user-attachments/assets/39350458-d15b-4615-85f9-85ea5b25662d)

![image](https://github.com/user-attachments/assets/d2cfc242-4230-432c-9853-a40fad6b93af)

---

## Summary from Breakout Room Discussion on Regex and Quantifiers
![image](https://github.com/user-attachments/assets/18e36fe9-246e-4229-8c72-3a26766ef5e2)
