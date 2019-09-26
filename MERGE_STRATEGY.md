# Merge Strategy

We can't start merging one by one blindly.

## Lexicon :

- **phr00t** = the fork made by Phr00t
- **xen2** = xen2's original repo
- **fdrobidoux** = my fork of xen2's repo, for the merge
- *^ When I refer to the authors, it'll be more obvious.*

## Steps :

1. Find the earliest commit by Phr00t that hasn't been merged yet.
2. Make a branch for that commit like `merge/{shorthash}-{one-or-two-words-describing-what-it-features-or-adds}`
3. For each file modified :
	1. For each change :
        - Regardless of the type of change
            - Check in fdrobidoux if it has a `// MERGE:` comment in its context (function-wide, for the line, for the entire class), and if so, ignore the change.
            - In doubt, consult xen2/phr00t directly for assistance.
        - If the change is a new function/property/field/etc. added
            - Check if newer version of function exists in a later commit (Annotate/blame) in phr00t, and if so, take that version instead.
            - Merge to fdrobidoux.
            - if any refs are missing
                - find if there is anything we can replace it with.
            - Add comment at beginning of new function like "// MERGE: Done (whole function)"
        - If the change is an added line in a function.
            - If it has changed at a later date from when the commit was made, at the same spot in phr00t (annotate/blame)
                - Use that latest version of the function for merge.
            - Diff/Merge phr00t version of the function into fdrobidoux version of the function.
            - If there is no merge conflicts
                - Keep the merge !
            - If there are merge conflicts
                - Analyse intentions in latest xen2 (annotate/blame)
                - Modify code manually to make it work.
            - Add "// MERGE: Done" at beginning of function.
        - If the change is a new class
            - Add it in.
            - if any refs are missing
                - Find if reference exists in phr00t.
                - If it does, add it to fdrobidoux. Refer yourself to steps at `For each change:` for it.
                - if it doesn't, then the ref was removed from xen2.
            - TODO: THE REST OF THIS

Finally, remove every `// MERGE:` comment using solution-wide refactoring, push it all to remote/origin/master, and make a pull request to `xenko3d/xenko`.

And we're done !!!
