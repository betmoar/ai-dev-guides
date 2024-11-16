When asked to commit changes to a Git repository, follow these detailed steps to prepare and finalize a well-documented commit.

# Steps

1. **Update Documentation and Changelog**:
   - Add relevant updates to `changelog.md` describing what was changed. Be clear and concise about the modifications made.
   - Update any other related documentation to reflect new features, changes, or fixes.

2. **Stage All Files**:
   - Prepare all modified, new, or deleted files for commit using `git add` to include them in the next commit.

3. **Craft a Proper Commit Message**:
   - Write a descriptive commit message that summarizes the changes. Follow these guidelines:
     - Use an imperative tone (e.g. "Fix bug that caused crash on save").
     - Limit the first line to 50 characters.
     - Optionally, provide additional information in the following lines after a blank line.
 
4. **Commit with Documentation Update**:
   - Ensure the final commit includes all changes, documentation updates, and use the crafted commit message.

# Output Format

- `changelog.md` should have a new entry reflecting the latest modifications.
- Commit message should be a short, precise summary of the changes:
  - **Summary line**: One line summarizing the changes made.
  - **Body (Optional)**: You can provide further details including:
    - **What**: A description of what was changed.
    - **Why**: Reason for the change, if not obvious.

# Example

**Prompt Input:**
"Add a new feature that enables exporting data to CSV."

**Steps Completed**:

1. Update `changelog.md`:
   - Add a new entry: "Added functionality to export data to CSV format."
2. Update documentation:
   - Edit relevant sections to explain how to use the CSV export feature.
3. Stage all files:
   - Run: `git add .`
4. Write a descriptive commit message:
   - **Commit message**: 
     ```
     Add feature for exporting data to CSV

     - Created a new CSV export utility that allows users to download data as CSV.
     - Updated necessary documentation and included tests for the export functionality.
     ```

# Notes

- Ensure that the commit message adheres to the project’s guidelines for style.
- The changelog entry should be succinct, describing exactly what changed from the user’s perspective.
- Remember to provide the "Why" for complex changes to maintain long-term clarity.