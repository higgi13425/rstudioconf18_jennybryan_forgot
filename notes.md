Notes - Things They Forgot to Teach You In R, rstudio::conf18
================
Jessica Minnier
1/31/2018 and 2/1/2018

Thanks to the excellent contributions (via `pull` request\!) from
classmate [Peter Higgins\!](https://github.com/higgi13425)

# Links:

Materials: [rstd.io/forgot](https://github.com/jennybc/what-they-forgot)

To use “in building” mirror: `options(repos = c(CRAN =
"https://cran.rstudio.com/"))`

# Random thoughts

## Day 1: Morning - library exploration

  - JB has us go to issues and put emoji on OS, tests that we’ve signed
    into github\! also sees how many windows users there are
  - it’s ok that things take a long time
  - make things self explaining (good filenames - see
    <https://speakerdeck.com/jennybc/how-to-name-files>), don’t spend a
    lot of time writing wordy explainers that you have to maintain and
    won’t want to read later
  - organize your files and keep your readme up to date\!
  - “unless you can keep it current (maintain it), don’t write it”
  - it helps to know about your R installation and where packages go in
    order to make a package
  - new package `fs` (for ‘file system’), helps us work with file paths.
    note, don’t use paste() to work with file paths like they are
    strings, they are not\!

## Day 1: Mid-morning - file copying and naming, projects

  - turn off .RData loading and never ask to save .RData
  - restart R (Shift-Cmd-F10) often\!
  - no absolute paths
  - use a stable base: `here::here("data","raw-data.csv")` in your
    project directory, or `fs::path_home()`
  - form paths at runtime relative to a stable base
  - normalizePath() makes it work on both windows and mac
  - Rstudio set up a mirror for downloading packages **in** the
    building\! Whaaattt\!
  - use `basename` instead of `strsplit` to get name of file from a path
    (don’t have to specify  or /)
  - name files and directories as thing\_thing-info\_thing2 so for
    instance day\_session\_topic so you can order and delimit them later

## Side note from my own issues in moving this repo to github

How to add an existing Rstudio repo to github:

This has changed since
[git 2.9](https://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories),
now when you add remote and then pull you need a special option. This
only needs to happen if you added a Readme. Just don’t do this and life
will be
    easier.

    git remote add origin https://github.com/jminnier/rstudioconf18_jennybryan_forgot.git
    git pull origin master --allow-unrelated-histories

Most easy option from
[happywithgitr](http://happygitwithr.com/existing-github-last.html)

``` r
usethis::use_github()
```

## Day 1: Afternoon - git/github

  - git is scary but you should learn the 3 things you always have to do
    (commit, push, pull) and just do them over and over until you are
    comfortable (“get off the beach\!”)
  - easier to start from github then go to rstudio (sad)
  - if you are more of a visual thinker, you might like useing a
    graphical front end for git, like SourceTree or GitKraken
  - when you clone a repo in Rstudio and copy the ssh (or https) into
    the prompt, then press TAB, it will auto-fill the name of the repo
    into the next field\!
  - if you want to collaborate on someone else’s repo, best practice to
    (1) fork their repo so you have a copy in your GitHub (2) then clone
    this to your local git repo. This will keep links, so that later you
    can push your changes to your GitHub repo and then issue a pull
    request to original owner.
  - in git commit: two yellow question marks: local file git has never
    seen before
  - jenny commits her .Rproj (this is controversial)
  - intermediate step “staging” tells git you do want these files to be
    part of the next commit, this way you can commit files separately.
  - Staging - put things that are ready to mail in a box, Commit - mail
    the whole box.
  - use conventional file extensions so that github can show you
    customized diffs
  - jenny thinks putting derived products in version control is a good
    idea (i.e. html from Rmds), but not binary files (word files, pdfs)
  - jim hester will show us how github makes it easy to search code
  - when using workbook button from .R files we get a html report (jenny
    says html maybe not best option, more later)
  - note to knit to pdf, start by installing tinytex package, then run
    tinytex::install\_tinytex, then you are able to knit to PDF
  - oh yeah, html does not look good on github =( too raw\!
  - mullet: what you need to write (.R, .Rmd) = this business in front;
    what you want to read/see (.html, .md) = party in the back (or is it
    the other way around?)
  - .html is not useful but .md is very useful for github; use YAML:

<!-- end list -->

    #' ---
    #' output: github_document
    #' ---

  - now github will render the resulting .md file this to look pretty
    nice\!
  - source: only hard-liners say don’t version control output (only
    source code). but having .md files or .html files makes it really
    useful to see what the output looks like and how it changes.
  - JB takeaway 1: if you want to make your stuff immediately
    consumable, rendering to markdown and commiting that at the same
    time as the R file, gives something others can look at with little
    to no effort (be kind and be realistic\!)
  - JB takeaway 2: markdown is vastly more useful than .html and .pdf
    (on github)
  - More about github\_documents
    [here](http://rmarkdown.rstudio.com/github_document_format.html)
  - files that look nice in github: .csv, .png, .md, see the
    browsability section of happywithgitr

## Day 1: Afternoon after break

  - to upload an existing git directory to github without going through
    all the steps, just do `usethis::use_github()`\!\!\!
  - JB showing that .R and .Rmd can make same github\_document output
  - You can make your README.md into a webpage by changing settings in
    GitHub. Go to your repo, click ‘Settings’, scroll way down to GitHub
    pages, change Source to Master, and choose a theme. Can add links to
    other .md files in the same repo by inserting this into README.md
    file: [displayname](link.md)
  - Good options for knitr:

<!-- end list -->

``` r
knitr::opts_chunk$set(
          collapse = TRUE,
          comment = "#>",
          out.width = "100%"
)
```

  - git can detect simple push conflicts (i.e. you forgot to pull first)
  - if you are collaborating on code: commit and push (and pull) often,
    so that you make small changes that git’s troubleshooting push fail
    algorithm can handle it; “sync to the mothership really often”
  - also working with binary files like pdf makes this really hard since
    git can’t look inside them to figure out what the problem is. so,
    don’t put them in your repo very often\! (.gitignore)
  - use githooks to avoid pushing files that have conflicts (they can
    look for the markers from the merge conflict)
  - if you have made conflicting commits to your local version and
    remote version, push will be rejected. Pull first and fix conflicts.
    If this does not work, consider git reset. If this does not work,
    consider renaming local repo to borked-repo, pull remote, then
    selectively copy over new useful files from borked-repo
  - you can search github for code snippets (I need to do this more\!),
    such as: [“llply” user:cran
    language:R](https://github.com/search?l=r&q=%22llply%22+user%3Acran+language%3AR&ref=searchresults&type=Code&utf8=%E2%9C%93);
    Jim Hester will talk more about this tomorrow

## Day 2 Morning - Jim Hester, searching github

  - Jim Hester is teaching us how to use github search, for example
    `read_csv OR read_delim col_type language:R extension:.R` looks for
    examples of using the `col_type` argument in `read_csv` or
    `read_delim` functions
  - if the documentation doesn’t answer your questions, use github
    search to find examples
  - example search: `user:cran onAttach` will search CRAN packages that
    use the function `onAttach`
  - use `user:` field to search CRAN or tidyverse because those
    users/orgs keep track of all the packages on cran or tidyverse
  - if you get an error, you can search that error code string in the
    repo to determine what is causing it
  - The tidyverse packages typically name internal helpers with a
    trailing underscore.
  - JH has a package for this\!
    [jimhester/lookup](github.com/jimhester/lookup)

<!-- end list -->

``` r
library(lookup)
lookup(knitr::knit)
```

  - JB: if you are reporting a bug or requesting an addition, be as
    specific as possible

## Day 2 morning, JB start up files

  - re: installing packages after an update: you can install them
    organically as you go, this is a good way to perform “spring
    cleaning” (JB and \[@LucyStats\](twitter.com/lucystats) are in favor
    of this). However, Jim Hester has a package for this, too\!
    [jimhester/autoinst](github.com/jimhester/autoinst) (but maybe try
    not to break it/find issues ;))
  - github search for “dotfiles” shows people’s repos of dotfiles
  - very useful links from JB’s repo:
      - Kevin Ushey blog post on `.Rprofile` [RProfile
        Essentials](http://kevinushey.github.io/blog/2015/02/02/rprofile-essentials/)
      - Kevin’s [etc repo](https://github.com/kevinushey/etc) for
        dotfiles and the like
      - Shaun Jackman’s [dotfiles
        repo](https://github.com/sjackman/dotfiles)
  - examples of good options to turn on:
      - `warnPartialMatchAttr = TRUE`, etc = no autocomplete\!
      - `utils::rc.settings(ipck=TRUE)` = yes autocomplete package names
  - don’t load packages in .Rprofile because you will be using functions
    other people can’t without loading
      - though JB still loads “workflow packages” since low risk for
        irreproducible code: devtools, usethis, remotes, testthat,
        reprex
  - can populate description file automatically (see JB’s .Rprofile)
  - interesting package to maintain these types of files:
    [HenrikBengtsson/startup](https://github.com/HenrikBengtsson/startup)

## Day 2 Morning after break - github project example

  - github etiquette: use `#` in front of numbers to link to issues,
    words like “Fixes” are keywords that can close issues [see more on
    github](https://help.github.com/articles/closing-issues-using-keywords/)
  - plan for revisiting analyses/projects (like 10x more than you
    thought you would)
  - refine and extend\! make your code more readable, efficient,
    resilient, general
  - beware of monoliths\! i.e one script and a workspace, much better to
    break logic and ouput into smaller pieces; divide and conquer;
    i.e. making figures is separate from modeling
  - make scripts based on the different steps in the analysis pipeline
    (see slide 17
    [slides/day2\_slides2\_project-api.pdf](slides/day2_slides2_project-api.pdf))
  - make outputs separate based on their uses rather than a giant RData
    file
  - practice “safe paths”\! use `here` package to do this; works on my
    machine and on yours, also works with knitr and rmarkdown\!
    rmarkdown sets workign directory where .Rmd file is, but `here` can
    get around this if you have subdirectories

<!-- end list -->

``` r
library(here)
here()
here("day1_s1_explore-libraries")
cat(readLines(here("day1_s2_copy-files/","00_filesystem-practice_comfy.R")))
```

  - we had an excerise of forking a
    [repo](github.com/jennybc/packages-report) and adding code to files
    along with documentation in the readme.
  - there are R packages that are similar to `make`, such as remake
    (more to come after lunch)

## Day 2 Afternoon - make-like, live purrr coding, API example

  - you can view csv files in github (better to do this than opening in
    excel\!)
  - you can ammend commits if you haven’t pushed yet
  - github can show you diffs of .png files, useful for seeing
    progression of plots
  - having projects in smaller pieces allows people to come into the
    code at the middle
  - JB’s [repo solution](github.com/jennybc/packages-report-EXAMPLE)
  - the table of file organization in JB’s
    [readme](https://github.com/jennybc/packages-report-EXAMPLE/blob/master/README.Rmd)
    is quite useful
  - Kirill Muller is telling us about `drake`,
    [repo](https://github.com/krlmlr/drake-pitch) and
    [slides](https://krlmlr.github.io/drake-pitch/)
  - drake will look at your code and run what needs to be updated
  - make gives you all kinds of problems that drake does not
  - use `drake_plan()` to map out your analysis plan that needs to be
    updated
  - `drake::loadd()` can load data or an object or a plot, updated based
    on your plan
  - how much complexity can this handle? KM used to use remake, where
    you specify plans with YAML files, and he had YAML files up to 6 mb,
    so very complex workflows
  - JB live coding `purrr` here:
    [rstd.io/jenny-live-code](rstd.io/jenny-live-code), using dropbox
    with url trick to make it render in the browser: use the the `raw=1`
    query
    <https://www.dropbox.com/s/2b8mi4rir23pvnx/jenny-live-code.R?raw=1>
  - it took JB a long time to embrace `plyr`, she stuck with `apply` for
    a while, until she read the `plyr` paper and finally “got it”
  - get good at iteration, really really good\!
  - `repurrrsive` is a package to learn `purrr` based on recursive lists
  - API is good example since it comes as json which is inherently a
    list and cannot be a rectangle right away
  - lists: one bracket is how you get multiple things, 2 brackets is how
    you get one thing (via twitter via hadley’s workshop)
  - [BRRR](https://github.com/brooke-watson/BRRR): package to play sound
    snippets
  - `purrr:walk()` replaces a for loop + a function, either through a
    formula `~` or a function
  - `View(listname)` is great in Rstudio, much easier to look at than
    super long `str(listname)`
  - `str(listname, list.len=3)` and `str(listname, max.level=1)` make
    `str` more manageable
  - side note, `wesanderson` color palettes in `repurrrsive` are
    awesome\!
  - normally don’t grow things inside lists or else R will get slow,
    need to designate space in advance, but `map` and `lapply` deal with
    those bookkeeping tasks
  - return results “like so” = `map_*` such as `map_dbl`
  - `map_dfr(minis, '[', c("pants","torso","head"))` = get all these
    things and put them in a df\!
  - why use `map` over `lapply`? some syntaxical sugar that makes things
    simpler and shorter
  - `flatten_int` can flatten lists
  - `map_chr(,.default = NA)` sets a default value of NA if it is
    missing; but it doesn’t replace “” with NA
  - can’t use `map_chr` if `map` returns items with different
    lengths–you will get an error; if you tried `sapply` on this it
    would just give you a list back (maybe not what you are expecting\!)
  - code that can make list columns from map:

<!-- end list -->

``` r
library(repurrrsive)
tibble(
  name = map_chr(got_chars, "name"),
  titles = map(got_chars, "titles")
) %>% head
#> # A tibble: 6 x 2
#>   name              titles   
#>   <chr>             <list>   
#> 1 Theon Greyjoy     <chr [3]>
#> 2 Tyrion Lannister  <chr [2]>
#> 3 Victarion Greyjoy <chr [2]>
#> 4 Will              <chr [1]>
#> 5 Areo Hotah        <chr [1]>
#> 6 Chett             <chr [1]>
```

  - workflow:
      - do something easy with iterative machine
      - do real hard thing with one representative unit
      - do hard thing with iterative machine
  - `pmap` can iterate over every row of a data frame, including and
    most especially tibbles where you have list columns
  - after the break we will have “choose your own adventure” time

# Q’s

  - what about versioning data? for small to medium you can easily use
    github, might need to just keep it in a separate repo and git that,
    or might need to use gitfs for large file systems
  - in the analysis pipeline, if I want to generate an html (or pdf etc)
    file along with the github\_document, is there a way to always
    generate both? you can “keep md” but can you “keep
    github\_document”? Sort of, but you need to use
    `rmarkdown::render` (in theory, though JB can’t get it to work yet
    for github\_docs…)
  - why is `fs` package making my Rstudio crash every time I want to
    view an object created with it? May be related to this
    [issue](https://github.com/r-lib/fs/issues/58)
