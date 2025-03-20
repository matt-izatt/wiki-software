# chmod

The `chmod` command in Linux is used to **change file and directory permissions**. File permissions define who can **read**, **write**, or **execute** a file.

### Basic Syntax:

```bash
chmod [options] mode file
```

#### **Permission Types:**

* **r** – Read (4) – Allows viewing the contents of the file.
* **w** – Write (2) – Allows modifying the file.
* **x** – Execute (1) – Allows running the file as a program or script.

### **Changing Permissions Using Numeric (Octal) Mode**

Each permission has a numeric value:

* `4` = Read
* `2` = Write
* `1` = Execute

#### Format:

```bash
chmod 764 file
```

* First digit = Owner’s permissions
* Second digit = Group’s permissions
* Third digit = Other’s permissions

Example:

```bash
chmod 755 file
```

* `7` → Owner = Read (4) + Write (2) + Execute (1) = **7**
* `5` → Group = Read (4) + Execute (1) = **5**
* `5` → Others = Read (4) + Execute (1) = **5**



### **Changing Permissions Using Symbolic Mode**

Format:

```bash
chmod [who][operator][permissions] file
```

#### Who:

* `u` – User (Owner)
* `g` – Group
* `o` – Others
* `a` – All (user, group, and others)

#### Operators:

* `+` – Add permission
* `-` – Remove permission
* `=` – Set specific permission

#### Example:

```bash
chmod u+x file
```

* Add execute permission for the file owner.

```bash
chmod g-w file
```

* Remove write permission for the group.

```bash
chmod a=r file
```

* Set read-only permissions for everyone.
