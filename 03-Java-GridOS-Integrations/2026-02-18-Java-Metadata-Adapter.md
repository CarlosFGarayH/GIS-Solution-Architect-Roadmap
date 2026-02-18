# Java Integration: Designing the Generic Asset Adapter

## 🧩 Core Concept: The "GisAsset" Container
To replicate GE's **SQL Adapter** logic, I need a Java structure that holds VMDS data before inserting it into PostgreSQL.

### Why HashMap?
Since Smallworld attributes are dynamic (defined in CASE Tool), Java must use a `Map` to hold field names and values without hard-coding classes.

## 💻 Logic Snippet: The SQL Adapter Foundation (Java 17)

```java
import java.util.HashMap;
import java.util.Map;

/**
 * Acts as the 'Record Persistence' layer for the migration.
 * Maps logical CASE objects to relational rows.
 */
public class GisAsset {
    private String tableName; // From CASE Tool Logical Model
    private Map<String, Object> attributes; // name -> value

    public GisAsset(String tableName) {
        this.tableName = tableName;
        this.attributes = new HashMap<>();
    }

    public void mapAttribute(String key, Object value) {
        // Here we apply GE's 'Lift & Shift' logic
        this.attributes.put(key, value);
    }
}
