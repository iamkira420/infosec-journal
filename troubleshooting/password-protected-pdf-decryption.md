# 🛠️ Removing PDF Passwords via Terminal with `qpdf`

Sometimes you're handed a password-protected PDF — maybe a report, lab file, or certificate — and it's annoying to re-enter the password every time. If you *already know* the password and just want a decrypted copy for easier access, `qpdf` has your back.

Here’s how to do it:

### 📦 Step 1: Install `qpdf`

On most Linux distros (I use Debian):

```bash
sudo apt install qpdf
```

On macOS (via Homebrew):

```bash
brew install qpdf
```

Windows folks, my bad!

### 🔓 Step 2: Decrypt the PDF

Replace the placeholders below with your actual filename and password:

```bash
qpdf --password=yourpassword --decrypt protected.pdf unprotected.pdf
```

* `--password`: Your known PDF password.
* `--decrypt`: Tells `qpdf` to remove the encryption.
* `protected.pdf`: The password protected PDF file.
* `unprotected.pdf`: The new, unlocked output file.

### ✅ Example

```bash
qpdf --password=d@3m0n$ --decrypt secret_notes.pdf notes_unlocked.pdf
```

---

### ⚠️ Handle With Care

🔐 **Just because you *can* remove a password doesn’t mean you always *should.***

* Keep **sensitive documents** password-protected unless you *explicitly need* them decrypted.
* If you're working in shared environments or storing files in the cloud, **maintain encryption** where possible.
* This method is for **authorized use only**. Never use it to bypass access controls or tamper with protected content.

Use responsibly, stay secure. 🧠💻


### 🔐 Bonus: Protecting a PDF with a Password

Want to *add* a password instead of removing one? `qpdf` can handle that too — useful when sharing exported reports, CTF writeups, or sensitive briefs.

Here's the syntax:

```bash
qpdf --encrypt userpass ownerpass 256 -- input.pdf protected.pdf
```

* `userpass`: The password required to *open* the PDF.
* `ownerpass`: The password for full permissions (e.g. editing, printing).
* `256`: Encryption level (256-bit AES is solid).
* `--`: Separates options from file inputs.

### ✅ Example

```bash
qpdf --encrypt S3cur3Open AdminOnly123 256 -- report.pdf report_protected.pdf
```

This will:

* Require `S3cur3Open` to open the PDF.
* Grant extra permissions only if `AdminOnly123` is entered.
* Use AES-256 for strong encryption.

### 🧠 Pro Tips

* Keep the **owner password** different and stored securely — it's your override key.
* Pair this with `chmod` or secure cloud sharing for extra layers of defense.
* Use descriptive names like `*_protected.pdf` to avoid overwriting originals.


### 🧩 "What If I Only Have One of the Passwords?"

Understanding how `userpass` and `ownerpass` behave helps avoid confusion — or leverage the right access when collaborating.

* 🔓 **If you only have the `userpass`**:
  You can **open and read** the PDF, but you may be **restricted** from actions like printing, copying, or modifying — depending on how it was protected.

* 🛠️ **If you have the `ownerpass`**:
  You can **open the PDF without the user password**, and you have **full control** — editing, copying, removing security, etc.
  It’s essentially the *master key*.

* 🧪 **Testing both?**
  You can simulate this by swapping out `userpass` and `ownerpass` in `qpdf` and checking how your PDF viewer reacts to restricted permissions.

💡 If you're generating PDFs to share with limited permissions, always keep the `ownerpass` stored safely offline — it's your recovery option if someone forgets the open password.


