# 42_EF_Core_Migrations – MCQs

## EASY MCQs

### Q1. What is the primary purpose of "Migrations"?
A. To move data between servers.  
B. To create a version history of Database Schema changes corresponding to Code changes.  
C. To migrate code from C# to Java.  
D. To backup data.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
It allows evolving the database schema (add table, drop column) incrementally as the application evolves.
</details>

### Q2. `dotnet ef migrations add <Name>` does what?
A. Reads the current `DbContext` model, compares it to the previous migration snapshot, and generates C# code (`Up`/`Down`) for the difference.  
B. Updates the database immediately.  
C. Adds a library.  
D. Creates a controller.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
It creates the *plan* (the migration file) but does not execute it against the DB yet.
</details>

### Q3. `dotnet ef database update` does what?
A. Generates code.  
B. Compiles the app.  
C. Applies any pending migration files to the target database.  
D. Deletes the database.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** C
**Explanation:**  
It checks the `__EFMigrationsHistory` table to see what's applied, then runs the missing migrations in order.
</details>

### Q4. The `Up()` method in a migration file:
A. Defines how to apply the changes (move forward).  
B. Defines how to undo the changes (rollback).  
C. Defines startup logic.  
D. Uploads files.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Example: `CreateTable(...)`, `AddColumn(...)`.
</details>

### Q5. The `Down()` method is used for:
A. Rolling back or reverting the migration.  
B. Server downtime.  
C. Downloading data.  
D. Logging errors.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Undo logic: `DropTable(...)`, `DropColumn(...)`. Used if you `update` to a previous target.
</details>

---

## MEDIUM MCQs

### Q6. Where does EF store the history of applied migrations?
A. Text file on disk.  
B. `__EFMigrationsHistory` table in the database itself.  
C. Registry.  
D. It doesn't track history.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This ensures the database knows its own version state regardless of which machine connects to it.
</details>

### Q7. How do you generate a SQL Script for production deployment?
A. `dotnet ef migrations script`  
B. You must write it manually.  
C. `dotnet sql generate`  
D. Copy paste from C# files.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
Generates the raw SQL (idempotent if flagged) so DBAs can review and run it safely on prod.
</details>

### Q8. To remove the *last* migration (that hasn't been applied to DB yet):
A. Delete the file manually.  
B. `dotnet ef migrations remove`  
C. `dotnet ef undo`  
D. `Ctrl+Z`  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This safely removes the C# file and reverts the Model Snapshot to the previous state.
</details>

### Q9. If you change a Property Name in C# (`Name` -> `FullName`), EF Migrations usually defaults to:
A. Renaming the column (preserving data).  
B. Dropping the old column (data loss) and Adding a new column.  
C. Doing nothing.  
D. Asking for permission.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
EF interprets it as "One prop deleted, one added". You typically get a warning "Data Loss". You must manually edit the migration to use `RenameColumn` or use `HasColumnName("OldName")` first.
</details>

### Q10. "Idempotent" scripts (`--idempotent`) include logic to:
A. Run infinitely.  
B. Check if a migration has already been applied (`IF NOT EXISTS...`) before running it.  
C. Delete everything first.  
D. Run faster.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Crucial for pipelines. You can run the script against a DB that is partially updated, and it will only apply the missing parts.
</details>

---

## HARD MCQs

### Q11. Can you seed data using Migrations?
A. No.  
B. Yes, using `modelBuilder.Entity<T>().HasData(...)`. EF converts this into `INSERT` / `UPDATE` statements in the migration.  
C. Only with raw SQL.  
D. Only CSV files.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
This is "Model Seeding". It manages data similarly to schema.
</details>

### Q12. "Snapshot" file (`DbContextModelSnapshot.cs`) purpose?
A. Backup of data.  
B. Represents the *current* calculated state of the full C# model. Used to calculate the "diff" when adding the next migration.  
C. A photo.  
D. Performance cache.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Without this, EF would have to re-play every previous migration to know what the DB looks like. Snapshot is the "Current Truth".
</details>

### Q13. Applying migrations at runtime (`context.Database.Migrate()`) during App Startup:
A. Is recommended for all scenarios.  
B. Is convenient for dev/small apps, but risky for high-scale/containerized production (race conditions if multiple instances start simultaneously).  
C. Impossible.  
D. Deletes data.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Better to use an init container or CI/CD pipeline step (SQL script) to migrate for robustness.
</details>

### Q14. How to handle "Merge Conflicts" in Snapshot file on a team?
A. Ignore them.  
B. It is painful. Usually requires deleting the conflicting migration and re-generating it on top of the merged main branch.  
C. Git handles it automatically.  
D. Stop using migrations.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**  
Since the Snapshot is machine-generated code, merging lines manually is error-prone. Re-generating the fresh migration is the standard fix.
</details>

### Q15. `DropTable` in `Up()` means:
A. You deleted an Entity class from the model.  
B. You added an Entity.  
C. You renamed a property.  
D. A bug.  

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**  
If the C# class is gone, the migration assumes the table should be removed.
</details>
