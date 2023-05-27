# livebook_edits

## Edit livebook cells from your preferred text editor.

#### *WARNING!*

This is an experimental[^1] hack/proof of concept.
It relies on livebook internals and could break at any time.
The current version has limited[^2] editing capabilities.

#### What is this?

It's a livebook that lets you edit other livebooks using an external text editor.

#### Why not just use the in browser editor?

Livebook is great, but the in browser cell editor doesn't currently support VI keybindings[^3].  This lets me use my own customized editor to edit livebook cells.

#### How it works:

Once evaluated the notebook will create and watch for changes
in the directory ~/livebook_edits.  When it sees new or modified
markdown (.md) or elixir script(.exs) files in that folder it
will add their content to the end of the specified notebook section.

#### Usage:

* Open the notebook and evaluate it.

  * This will create a directory 'livebook_editor' in your home directory
    and start monitoring that directory for file changes.

* Create a new notebook.

  * Leave the default title "Untitled notebook" and the default section named "Section".

* Now in your text editor create a new file **~/livebook_edits/edit.exs[^4]** with the following content:

  ```
  IO.puts("Hello")
  ```

* Save the file and you should see a new cell appended to new "Untitled notebook" section "Section".

##### Targetting a specific notebook and section:

By default it will target a section named "Section" of the notebook titled "Untitled notebook".  You can target a different notebook and section by adding a comment on the first line:

```
# Notebook Name # Section Name
IO.puts("Hello, again.")
```

##### Append or replace cell:

By default a new cell will be appended at the end of the section.
You can replace the last cell in the section by appending '>' on it's own as the last line of the cell.

```
# Notebook Name # Section Name
IO.puts("Last cell's content will be replaced by this.")
>
```

##### Markdown cells:

To add a markdown cell, just create a file with the extension **.md** in the **~/livebook_edits** directory. e.g. **~/livebook_edits/edit.md**

```
# Notebook Name # Section Name
- Markdown content
- Goes here
```

[^1]: It works for my use case on a mac with livebook v0.9.2. Other configurations have not been tested. YMMV.

[^2]: Currently limited to either overwriting the last cell in a notebook section or appending a new cell at the end of a notebook section. I plan to add more capabilities in the future, but I find it is already useful, as is.

[^3]: More info here: https://github.com/livebook-dev/livebook/issues/715

[^4]: You can use any file name as long as it is inside the **~/livebook_edits** directory and has an **.exs** or **.md** extension.