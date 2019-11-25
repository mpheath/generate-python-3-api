# Frequently Asked Questions

**Q.** What does safe defaults imply?

**A.** The script will hopefully work first time without any changes to
the settings. Changes can be done once the script has proven to work.
If it does not work with changes, then you can try to isolate the changes
made to find the cause.
With importing many modules, no problems is good, though I know some of you
may experience problems, especially with site packages from 3rd parties.

---

**Q.** `settings['import_site']=1` causes import errors that affects the
script operation or generated output?

**A.** Packages downloaded from [PyPI] or other can be good to import in
this script, or can be an issue.
This is something that the script may have no control.
Success varies and I have had some that want a certain module loaded
before another is loaded.
To overcome this, you can try adding the module to the list of
`settings['include_modules_fullname_import_first']` to load that module first.
Some other modules may need to be excluded as they may be incapable of being
handled by the script.
You may need to be creative to overcome any issues.
Which is why the setting is `settings['import_site']=0` initially to be a
safe default.

---

**Q.** Why are dunder methods etc. not included as the safe defaults?

**A.** I consider dunder methods i.e. `__init__` etc. for advanced users.
The more entries added to the calltip files, the more that the user needs
to search and find what is wanted.
The more entries, the more burden put on the editor to handle.
You can have the dunder methods by allowing members with double underscores.
If you want to see many more entries, then try
`settings['inspect_members_more']=1` to get files up to 150 MB in total.
This will probably slow down the editor and your coding with the excessive
amount of entries. The safe default is to be just enough entries.

 [PyPI]: https://pypi.org/
