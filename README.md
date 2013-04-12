# webrev

This is a copy of the webrev code review tool found in
[illumos](http://www.illumos.org).  Like the rest of illumos, it's licensed
under the CDDL.

This version works on OS X and illumos-based systems.


## Usage

First, make sure all of your changes are committed (more than one commit is
okay).  Then just run "webrev" from inside your repo.  It will figure out what's
changed and generate a directory called "webrev" with an index.html that's a
completely offline code review browser.

For example, here are some changes:

    $ git status
    # On branch master
    # Your branch is ahead of 'origin/master' by 1 commit.
    #
    nothing to commit (working directory clean)

    $ git log -1 --name-only
    commit 8f34dc4bb923e62460052d0e895a98f097a0f85b
    Author: Dave Pacheco <dap@joyent.com>
    Date:   Thu Apr 11 16:54:50 2013 -0700

        sample changes

    README.md

Now, run webrev:

    $ webrev 
    WARNING: codereview(1) not found.
    WARNING: ps2pdf(1) not found.
       SCM detected: git
     File list from: git-active -p git@github.com:davepacheco/node-jsprim.git ... Done.
          Workspace: /Users/dap/work/node-jsprim/.git (at 8f34dc4bb923e62460052d0e895a98f097a0f85b)
    Compare against: git@github.com:davepacheco/node-jsprim.git
          Output to: /Users/dap/work/node-jsprim/webrev
       Output Files:
            README.md
                     patch cdiffs udiffs wdiffs sdiffs frames old new
     Generating PDF: Skipped: no output available
         index.html: Done.

and open the generated index.html:

    $ ls webrev/index.html 
    webrev/index.html

The HTML files in the webrev directory use only relative links, so you can move
the directory around wherever you want.


## Advanced options

You can use "-p" to specify the parent (upstream) to compare against.  This can
be a git URL or just a regular git expression, as in "webrev -p HEAD^^^^^".
