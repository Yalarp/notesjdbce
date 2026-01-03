# 06_Assemblies_And_GAC – MCQs

## EASY MCQs

### Q1. What is an Assembly in .NET?

A. A tool to write C# code.  
B. A compiled code library (.dll or .exe) used for deployment and versioning.  
C. A folder containing source files.  
D. The runtime environment (CLR).  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
An assembly is a compiled code library (either an executable `.exe` or a library `.dll`) that serves as the fundamental unit of deployment, version control, and security in .NET.
</details>

### Q2. Which component of an assembly contains the description of the assembly itself (version, files, etc.)?

A. MSIL Code  
B. Resources  
C. Manifest  
D. Type Metadata  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The **Manifest** contains metadata about the assembly itself, including the assembly name, version information, list of files, and referenced assemblies.
</details>

### Q3. What does GAC stand for?

A. General Assembly Compiler  
B. Global Application Cache  
C. Global Assembly Cache  
D. Generic Assembly Container  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
GAC stands for **Global Assembly Cache**. It is a machine-wide cache used to store assemblies that are intended to be shared by several applications on the computer.
</details>

### Q4. Which file extension represents a Dynamic Link Library assembly?

A. .cs  
B. .exe  
C. .dll  
D. .config  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
`.dll` (Dynamic Link Library) is the extension for assemblies that are code libraries (class libraries) and do not have a main entry point.
</details>

---

## MEDIUM MCQs

### Q5. What is the main difference between a Private Assembly and a Shared Assembly?

A. Private assemblies are encrypted; Shared are not.  
B. Private assemblies are placed in the application folder; Shared assemblies are placed in the GAC.  
C. Private assemblies must have a strong name; Shared assemblies do not.  
D. Private assemblies cannot contain classes.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Private assemblies are deployed in the application's directory and used only by that application. Shared assemblies are installed in the GAC and can be used by multiple applications.
</details>

### Q6. Which four items constitute a Strong Name?

A. Filename, File Size, Date, Author.  
B. Assembly Name, Version Number, Culture Information, Public Key Token.  
C. Namespace, Class Name, Method Name, Parameter Types.  
D. Assembly Name, CLR Version, Windows Version, Private Key.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
A strong name consists of the Assembly's text name, Version number, Culture information (for localization), and a Public key token (generated from a key pair).
</details>

### Q7. What are Satellite Assemblies used for?

A. To launch satellites.  
B. To store localized resources (like images and strings) for different cultures/languages.  
C. To connect to remote databases.  
D. To monitor application performance.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
Satellite assemblies contain only resources (no executable code) and are used for localizing applications into different languages (cultures).
</details>

### Q8. Which command line tool is used to manage the GAC (install/uninstall assemblies)?

A. csc.exe  
B. ildasm.exe  
C. gacutil.exe  
D. sn.exe  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
`gacutil.exe` (Global Assembly Cache Tool) is used to view, install, and remove assemblies from the Global Assembly Cache.
</details>

---

## HARD MCQs

### Q9. How does .NET solve the "DLL Hell" problem found in older Windows environments?

A. By forcing all DLLs to have the same filename.  
B. By using side-by-side execution, allowing different versions of the same shared assembly to coexist in the GAC.  
C. By preventing the use of DLLs entirely.  
D. By recompiling all applications whenever a DLL changes.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
.NET solves DLL Hell primarily through Strong Naming and the GAC, which allow multiple versions of the same assembly to exist side-by-side. Applications can bind to the specific version they were built with.
</details>

### Q10. What is the standard format for an Assembly Version number?

A. v1.0  
B. Year.Month.Day  
C. Major.Minor.Build.Revision  
D. Alpha.Beta.Gamma  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
The standard version format is `Major.Minor.Build.Revision` (e.g., 1.0.0.0). Major/Minor indicate feature changes, while Build/Revision indicate bug fixes or updates.
</details>

### Q11. Which tool would you use to view the Metadata and MSIL code within an assembly?

A. notepad.exe  
B. ildasm.exe  
C. sn.exe  
D. gacutil.exe  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** B

**Explanation:**  
`ildasm.exe` (IL Disassembler) is the tool used to inspect the internal structure of an assembly, including its Manifest, Metadata, and MSIL code.
</details>

### Q12. To install an assembly into the GAC, what requirement must be met?

A. It must be an executable (.exe).  
B. It must be smaller than 1MB.  
C. It must have a Strong Name.  
D. It must be written in C#.  

<details>
<summary><strong>Answer</strong></summary>

**Correct Answer:** C

**Explanation:**  
Only assemblies with a **Strong Name** (signed with a private key) can be installed into the Global Assembly Cache (GAC). This ensures integrity and unique identification.
</details>

All MCQs were generated strictly from the provided notes with answers hidden and no syllabus deviation.
