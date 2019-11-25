# Customize Settings

The default settings in the script are safe defaults. That is, SciTE does
not allow escapes in Calltips by default, so the default settings in the script
relate to this. Long call signatures are not wrapped to another line and the
doc description is only a single line.

These settings would be changed for my use:

 * `calltip_use_escapes=1`<br>
   I have the SciTE property setting of `calltip.python.use.escapes=1` set.

 * `doc_line_count=-1`<br>
   This setting has many worthy values, though if you want multiple doc lines
   then this will try to get the first paragraph.

 * `escape_long_signatures=1`<br>
   Some call signatures are very long, so this is good to set if you do not
   want the calltips going off screen.

 * `replace_commas_in_parameters=1`<br>
   SciTE typcally separates parameters by comma. If a comma is in the parameter,
   then this alternative comma will not be detected as a parameter separator.

 * `replace_parentheses_in_parameters=1`<br>
   SciTE typcally ends the call signature at the first closing parentheses.
   If a parameter has a closing parentheses, then this alternative closing
   parentheses will not be detected as the end of the call signature.

 * `space_before_doc_api=0`<br>
   The space may look good in python3.api, though in the calltip, it can be
   unneeded. This is just a visual preference.

The last 3 settings above only applies to python3.api used in SciTE.

Example calltip with default settings in SciTE:

```
subprocess.Popen(args, bufsize=-1, executable=None, stdin=None, stdout=None, stderr=None, preexec_fn=None, close_fds=True, shell=False, cwd=None, env=None, universal_newlines=None, startupinfo=None, creationflags=0, restore_signals=True, start_new_session=False, pass_fds=﴾﴿, *, encoding=None, errors=None, text=None)
[class] Execute a child program in a new process.
```

As you can see, it is very long and a space is before the doc description.

This is all settings applied above except for `replace_commas_in_parameters=0`
and `replace_parentheses_in_parameters=0` as default:

```
subprocess.Popen(args, bufsize=-1, executable=None, stdin=None, stdout=None,
 stderr=None, preexec_fn=None, close_fds=True, shell=False, cwd=None, env=None,
 universal_newlines=None, startupinfo=None, creationflags=0, restore_signals=True,
 start_new_session=False, pass_fds=()
, *, encoding=None, errors=None, text=None)[class] Execute a child program in a new process.
```

An improvement based on the allowed calltip width, though the signature ends at
`pass_fds=()` even though it is not the end that is wanted.

Fix this by applying all changes to the settings:

```
subprocess.Popen(args, bufsize=-1, executable=None, stdin=None, stdout=None,
 stderr=None, preexec_fn=None, close_fds=True, shell=False, cwd=None, env=None,
 universal_newlines=None, startupinfo=None, creationflags=0, restore_signals=True,
 start_new_session=False, pass_fds=﴾﴿, *, encoding=None, errors=None, text=None)
[class] Execute a child program in a new process.
```

Now it looks better and even the highlighting of current parameter up to the
last parameter works as it should. I notice the closing parentheses may display
as an opening parentheses in some calltips when using the replacement commas
and parentheses. I consider this as a display bug not related to the script,
as some editors show the bug while others do not. Still, the fix seems
better than if it were not applied.

Notepad++ uses XML files which can support newlines by use of an entity and
the script inserts each parameter into separate XML tags, so the display of
calltips is good. Change settings `calltip_use_escapes=1` to allow
`escape_long_signatures=1` to be set. And setting `doc_line_count=-1` will
display the doc description as multiple lines of the first paragraph.

If you want to adjust the calltip display in Notepad++ like with SciTE
shown above, view the settings `space_before_doc_xml` and
`space_before_parameter_xml`. I could have merged the settings together
for both editors, though the calltip display of both are similar,
they are not the same.

Note:

```python
# Make Notepad++ files.
if sys.platform == 'win32':
    calltips.make_npp_files()
```

Copied from the main code section at bottom of script. If you want to make
Notepad++ XML files with Linux, then remove the win32 conditional check.
The check exists only as Notepad++ is not expected to be used on Linux.

