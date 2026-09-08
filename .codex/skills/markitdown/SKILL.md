---
name: markitdown
description: Convert local documents and media into Markdown for analysis, indexing, or editing. Use when a task requires extracting content from PDF, DOCX, PPTX, XLSX, HTML, images, audio, or other MarkItDown-supported files.
metadata:
  short-description: Convert files to Markdown with MarkItDown
---

# MarkItDown

Use the MarkItDown Python package to convert supported files into Markdown before analyzing or transforming their content.

## Setup

Install the declared dependency before first use:

~~~bash
python -m pip install -r requirements.txt
~~~

The requirements file installs MarkItDown with all optional format integrations. If the task needs only a small subset, install a narrow extra such as markitdown[pdf,docx,pptx].

## Workflow

1. Identify the input file and confirm that it is in the task's scope.
2. Convert it with the MarkItDown CLI or Python API.
3. Preserve generated Markdown in the task's working area when it will be reused.
4. Analyze or edit the Markdown, keeping the original unchanged unless the user explicitly asks for replacement.
5. Report conversion failures clearly and fall back to a format-specific reader only when needed.

CLI example:

~~~bash
markitdown path/to/input.pdf -o work/input.md
~~~

Python example:

~~~python
from markitdown import MarkItDown

converter = MarkItDown()
result = converter.convert('path/to/input.docx')
markdown = result.markdown
~~~

## Safety

MarkItDown performs I/O with the privileges of the current process. Treat input files and URLs as untrusted: do not convert an unapproved path or remote resource, and do not expose secrets found in converted content. Prefer local, user-provided files and the narrowest conversion function that meets the task.

Do not enable MarkItDown plugins unless the user requests plugin-based conversion and the plugin source is trusted. Never execute converted Markdown as code.

## Output

Keep intermediate conversions under the task's working directory. Use user-facing output locations only for final deliverables. Cite the original input path when summarizing extracted content.