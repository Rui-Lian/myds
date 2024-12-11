Here’s a comprehensive tutorial on how to use the **Dataview** plugin in Obsidian, covering installation, basic queries, and practical examples.

## Installing Dataview

1. **Open Obsidian Settings**:
   - Click on the **Settings** icon in the bottom left corner.

2. **Enable Community Plugins**:
   - Navigate to the **Community plugins** tab.
   - Toggle on **Safe mode** if it's currently enabled.
   - Click on **Turn on community plugins**.

3. **Install Dataview**:
   - Use the search bar to type **dataview**.
   - Click on the Dataview plugin and then hit **install**.
   - After installation, click **enable** to activate the plugin.

4. **Configure Settings**:
   - Go to the Dataview settings and enable options like **JavaScript Queries** and **Automatic Task Completion** for enhanced functionality.

## Creating a Dataview Code Block

1. **Open or Create a Note**:
   - Start a new note or open an existing one in your Obsidian vault.

2. **Add a Code Block**:
   - Type three backticks (```) to create a code block.
   - Specify `dataview` for standard queries or `dataviewjs` for JavaScript queries.

3. **Edit the Code Block**:
   - Click on **edit this block** at the top right to enter your query.

## Writing Queries

### Basic Structure
A basic Dataview query follows this structure:

```markdown
```dataview
TABLE file.name AS "File Name"
FROM "FolderName"
WHERE file.name = "Example Note"
SORT file.ctime DESC
```
```

### Key Components

- **Type of Query**: Specify whether you want a `table`, `list`, or `task`.
- **Fields**: Define which fields to display (e.g., `file.ctime` for creation time).
- **Source**: Use `FROM` to specify where to pull data from (a folder or specific notes).
- **Conditions**: Use `WHERE` to filter results based on certain criteria.
- **Sorting**: Use `SORT` to order your results by specific fields.

### Example Queries

1. **List All Notes in a Folder**:
    ```markdown
    ```dataview
    LIST
    FROM "MyFolder"
    ```
    ```

2. **Table of Tasks with Completion Status**:
    ```markdown
    ```dataview
    TABLE file.link AS "Task", status AS "Status"
    FROM "TasksFolder"
    WHERE status = "Incomplete"
    SORT file.cday ASC
    ```
    ```

3. **Querying with Inline Fields**:
   You can also use inline fields within your notes. For example, in a note, you might have:
   ```markdown
   ---
   project: "Project A"
   status: "In Progress"
   ---
   ```
   Then query it like this:
   ```markdown
   ```dataview
   TABLE project, status
   FROM "Projects"
   WHERE status = "In Progress"
   ```
   ```

### Additional Tips

- Use `group by` to categorize results (e.g., group tasks by their completion status).
- Rename columns using `AS` followed by your desired name (e.g., `file.link AS "Link"`).
- To remove default ID columns, use `WITHOUT ID`.

## Practical Use Cases

1. **Creating a Reading List**: 
   You can create a list of books or articles you want to read by tagging them appropriately and querying based on those tags.

2. **Tracking Tasks and Projects**: 
   Use Dataview to pull all tasks from various notes into one comprehensive list, allowing you to manage your workload effectively.

3. **Dynamic Dashboards**: 
   Build dashboards that summarize various aspects of your notes, such as recent changes, upcoming deadlines, or project statuses.

## Conclusion

The Dataview plugin significantly enhances Obsidian's capabilities by allowing users to treat their notes as a database. By following this tutorial, you should be able to install Dataview, write basic queries, and apply them in practical scenarios within your Obsidian vault. For more advanced features and customization options, refer to the official [Dataview documentation](https://blacksmithgu.github.io/obsidian-dataview/).

Citations:
[1] https://eastbournetrampoline.com/obsidian-dataview-for-beginners/
[2] https://www.youtube.com/watch?v=8yjNuiSBSAM
[3] https://www.youtube.com/watch?v=JTObSymEvWA
[4] https://publish.obsidian.md/tasks/Other+Plugins/Dataview
[5] https://www.youtube.com/watch?v=G8eOF61wmzI
[6] https://forum.obsidian.md/t/a-case-against-dataview-a-story/82210