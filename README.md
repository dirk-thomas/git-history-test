# Preserve history when moving / splitting / copying files in a git repository

Consider the following cases:

* The original file `foo` is not needed anymore but its content should continue to be used in N new files (e.g. `bar` and `baz`):

  * First commit:
    * Duplicate the content without any changes: `cp foo bar`, `cp foo baz`
    * Add the new files, remove the old file: `git add bar bar`, `git rm foo`
  * Following commits:
    * Apply arbitrary changes to the new files and still be able to see the full history:
      * Blame [bar](https://github.com/dirk-thomas/git-history-test/blame/split-into-new-files/bar)
      * Blame [baz](https://github.com/dirk-thomas/git-history-test/blame/split-into-new-files/baz)
  * :thumbsup:

* The original file `foo` is still needed but parts of the content should be copied / moved to a new file (e.g. `bar`):

  * First commit:
    * Duplicate the content without any changes: `cp foo bar`
    * Add the new file: `git add bar`
  * Following commits:
    * Apply arbitrary changes to the new file but you can't see the full history anymore:
      * Blame [bar](https://github.com/dirk-thomas/git-history-test/blame/extract-part-into-new-file/bar)
  * :thumbsdown:

  * First commit:
    * Duplicate the content without any changes: `cp foo dummy`
    * Add the new dummy file, remove the old file: `git add dummy`, `git rm foo`
  * Apply the first option:
    * Duplicate the content without any changes: `cp dummy foo`, `cp dummy bar`
    * Add the new files, remove the old dummy file: `git add foo bar`, `git rm dummy`
  * Following commits:
    * Apply arbitrary changes to the new files and still be able to see the full history:
      * Blame [foo](https://github.com/dirk-thomas/git-history-test/blame/extract-part-into-new-file-with-extra-step/foo)
      * Blame [bar](https://github.com/dirk-thomas/git-history-test/blame/extract-part-into-new-file-with-extra-step/bar)
  * :thumbsup:
