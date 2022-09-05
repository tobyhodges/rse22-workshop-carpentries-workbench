---
title: The Carpentries Workbench
teaching: 45
exercises: 20
---

::::::::::::::::::::::::::::::::::::::: objectives

- Identify the key tools used in The Carpentries lesson infrastructure.
- Complete the fundamental setup steps for a new lesson repository.
- Find the most important source files for a lesson website.
- Edit the RMarkdown source of an episode using RStudio.
- Build and view a local version of a lesson website.
- Preview the changes to a rendered lesson in a Pull Request.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How is a lesson site set up and published with GitHub?
- What are the essential configuration steps for a new lesson?
- How do you create and modify the pages in a lesson?
- How do you preview changes made to a lesson?

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::: prereq

This episode requires you to have R and Git installed on your machine.


::::::::::::::::::::::::::::::::::::::::::::::::::

- create repo on GitHub from Rmd template
- tour that, then clone locally
- create_episode
- preview
- push
- open pull request

In this next part of the workshop, we will explore the new infrastructure for lessons -
The Carpentries Workbench.
In this section, you will learn about the key components of the Workbench
and gain some hands-on experience of creating and editing a lesson website
using the Workbench.

## GitHub Pages

The source of all The Carpentries lessons is made publicly-available in repositories on [GitHub].
By making our repositories public like this,
we encourage others to help us maintain and improve our lessons,
and make it as easy as possible for them to re-use and modify our lessons for their own purposes.

Via a system called **GitHub Pages**, users can build and host websites 
from the files present in any repository on GitHub.
For many years, 
this has been how The Carpentries presents its lesson websites to the world.

## Using The Carpentries Workbench

Carpentries lesson websites are built with [**The Carpentries Workbench**][workbench],
a toolkit that converts Markdown and RMarkdown files into the HTML
that can be served by GitHub Pages.

### Creating a Lesson Repository

To get started, we first need to create a new repository for our lesson.
We will use a template to do this, 
so that the new repository contains the basic files and folders
that the Workbench needs in order to build a lesson site.
There are currently two templates to choose between:

1. [A Markdown template][md-template], suited for lessons that do not need to contain executable code.  
2. [An RMarkdown template][rmd-template], best suited to lessons that will include R source code that will generate output.

We are going to use the **RMarkdown template** in this workshop.

::: challenge

## Creating a new lesson repository

Follow the steps demonstrated by the workshop lead:

1. [generate a new repository from the Rmd lesson repository template][rmd-template-generate]
2. complete the configuration for that new repository:
   * Add a name for the repository
     * The name should be descriptive but fairly brief,
       with hyphens (`-`) to separate words
     * The name can always be changed later, via the repository settings
   * In the "Description" field, write the title of your lesson
   * Choose "Public" visibility
   * **Make sure the "Include all branches" box is checked**. This is not
     required, but means that the setup on GitHub pages moves faster initially.

After pressing the _Create repository using this template_ button,
you should be presented with a brand new lesson repository.

:::


### Repository Files

The repository contains a number of files and folders. The most important files
and folders are:

 - `episodes/` contains the main narrative content of the lesson
 - `instructors/` contains information useful for instructors such as instructor
   notes relevant for the overall lesson or extra exercises that could be useful
   for learners who would like an extra challenge

Most of these are source files for the content of our new lesson,
but a few are accompanying files primarily intended for the repository itself
rather than the lesson website.
These are:

- `CODE_OF_CONDUCT.md`
- `CONTRIBUTING.md`
- `LICENSE.md`
- `README.md`
- `.gitignore`
- and the `.github/` folder.

We will address all of the files later in the workshop.
For now, we will move on to complete the basic setup of the lesson.

### Configuring a Lesson Repository

#### Activating GitHub Pages

We need to tell GitHub to begin serving the lesson website via GitHub Pages.
To do this, navigate to _Settings_, then choose _Pages_ from the left sidebar.
Under _Source_, choose the `gh-pages` branch, leave the folder set to `/ (root)`,
and click _Save_.
Now, copy the URL in the box: this will be the address of your lesson site.

::: callout

### Which branch to use?

Although we configure GitHub Pages to serve the lesson website from the `gh-pages` branch,
**the default working branch for a lesson will be `main`**.
For the rest of this training, you should add and edit files on `main`,
and in future, when you open Pull Requests to update the lesson content,
these should also be made to `main`.
The `gh-pages` branch should never be modified by anyone other than the automated actions-user account.

:::

Returning to the repository home page 
(e.g. by clicking the name of the project near the top left of the window),
click the gear wheel icon near the top right, to edit the _About_ box.
Paste the Pages URL into the _Website_ box and click _Save changes_.

After following these steps, when you navigate to the pages URL, you should be see a lesson website with The Carpentries logo and "Lesson Title" in the top-left corner.
You may need to wait a few minutes for the website to be generated.

#### `config.yaml`

The lesson title can be adjusted by modifying the `config.yaml` file in the repository.
The `config.yaml` file contains several global parameters for a lesson---to
determine some of the page styling, contact details for the lesson, etc---and 
is written in _[YAML]_, a structured file format of key-pair values.
As well as the title of the lesson,
you can and should adjust some of [the other values in `config.yaml`][set-config],
but you should not need to add new values or learn a lot about YAML 
to be able to configure your lesson.

::: challenge

### Practice with `config.yaml` (5 minutes)

Complete the configuration of your lesson by adjusting the following fields in `config.yaml`:

- `email`: add an email address people can contact with questions about the lesson/project.
- `created`: the date the lesson was created (today's date) in YYYY-MM-DD format.
- `keywords`: a (short) list of keywords for the lesson, 
   which can help people find your lesson when searching for resources online.
- `source`: change this to the URL for your lesson repository.

We will revisit the `life_cycle` and `carpentry` fields in `config.yaml` later in this training. 

:::

::: callout

### Improving the `README.md`

The `README.md` file is the "front page" of your lesson repository on GitHub,
and is written in Markdown.
You should use it to provide basic information about the project,
for anyone who finds their way to the source files for your lesson.
Although we do not have time in this workshop,
if you intend to keep working on your lesson when you leave,
we recommend that you take a few minutes to update 
the README with some basic information about the project, e.g.:

- the lesson title
- a short description of the lesson
- a list of the names of the authors, optionally linked to their GitHub profile

:::


## Working with a Local Copy

Before we explore the source files for the content of a lesson,
we will make a copy of the new lesson repository on our local system.
To do so, we need to _clone_ the repository to a place on our system
where we can find it easily.

In the example below, we clone the repository to our user's `Desktop` on our
filesystem, using the SSH protocol. (If you configured a personal access token
for authenticating to GitHub, instead of SSH keys, you should use the HTTPS
protocol.)

```bash
cd ~/Desktop
git clone git@github.com:USER_NAME/REPOSITORY.git
```

Now that we have a copy of the lesson repository locally,
we need to make sure that we have everything we need to continue
working with that repository on our own system.

## Installing the Workbench

1. Open RStudio
2. In the console, type the following commands:

```r
# register the repositories for The Carpentries and CRAN
options(repos = c(
  carpentries = "https://carpentries.r-universe.dev/",
  getOption("repos")
))

# Install the template packages to your R library
install.packages(c("sandpaper", "varnish", "pegboard", "tinkr"))
```

::: prereq

### For Linux Users

If you have a linux system, you may need to install C libraries that
the workbench dependencies require (such as libxml). A set of dependencies for
ubuntu can be found using the following command:

```bash
curl https://carpentries.r-universe.dev/stats/sysdeps 2> /dev/null \
| jq -r '.library' 
```

:::


3. Test your installation:

```r
library('sandpaper')
library('fs')
library('rmarkdown')
rmarkdown::pandoc_version()
tmp <- tempfile()
sandpaper::no_package_cache()
sandpaper::create_lesson(tmp, open = FALSE)
sandpaper::build_lesson(tmp, preview = FALSE, quiet = TRUE)
fs::dir_tree(tmp, recurse = 1)
```

```output
[1] ‘2.12’
ℹ Consent for package cache revoked. Use `use_package_cache()` to undo.
ℹ No schedule set, using Rmd files in episodes/ directory.
→ To remove this message, define your schedule in config.yaml or use `set_episodes()` to generate it.
✔ First episode created in /tmp/RtmpxeJyVD/file45677ea639b2/episodes/introduction.Rmd
ℹ Workflows up-to-date!
✔ Lesson successfully created in /tmp/RtmpxeJyVD/file45677ea639b2
/tmp/RtmpxeJyVD/file45677ea639b2
/tmp/RtmpxeJyVD/file45677ea639b2
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE.md
├── README.md
├── config.yaml
├── episodes
│   ├── data
│   ├── fig
│   ├── files
│   └── 01-introduction.Rmd
├── index.md
├── instructors
│   └── instructor-notes.md
├── learners
│   └── setup.md
├── links.md
├── profiles
│   └── learner-profiles.md
└── site
    ├── DESCRIPTION
    ├── README.md
    ├── _pkgdown.yaml
    ├── built
    └── docs
```


If everything looks ok (e.g. no warnings or errors), we can go ahead and open the lesson repository as
a project in RStudio (_File_ -> _Open Project..._).

::: callout

### Having Trouble?

If you are having trouble installing a particular component of the workbench,
we have created an RStudio cloud instance that you can use to follow along
with the desktop commands: <https://rstudio.cloud/content/4442910>. 

:::



## Lesson Content Source Files 

Using the _Files_ tab within RStudio, 
we can begin to look at where the content of a lesson is stored and written.

The **"home page" of a lesson is created from the `index.md` file**:
this file should contain a brief introduction to the lesson, 
designed to give visitors to the page a first impression of the lesson
and whether it is appropriate for them.


**The main body of the lesson is written in _episodes_**: 
the individual chunks or sections that the lesson is separated into.
The episode pages of the lesson site will be constructed from Markdown files
in the `episodes` folder of the lesson repository.

The `episodes` folder of the new repository contains a single file,
`01-introduction.Rmd`. 
The content of this file includes examples of how to write RMarkdown files
for The Carpentries Workbench.

There are two important things to note:

1. The file begins with a short header, 
   written in the same key-value pair syntax we encountered in `config.yaml`.
   The fields in this header describe the episode title and the estimated time (in minutes)
   required to teach it and complete the exercises.
2. The example content begins after the blank line that follows this header.
   It includes several lines that start with strings of colons (`:::::::`).
   These mark the beginnings and ends of structural elements within the page, 
   called _fenced divs_. 
   Each fenced div starts and ends with a string of colons. 
   A word at the end of the starting colons indicates what kind of block it is. 
   Fenced divs are used for a variety of different blocks of content,
   including:
   * challenges and solutions
   * instructor notes
   * callouts i.e. optional content that can provide extra context 
     or answer a frequently asked question about a particular topic in a lesson


```markdown
---
title: "Using RMarkdown"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do you write a lesson using RMarkdown and `{sandpaper}`?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain how to use RMarkdown with The Carpentries Workbench
- Demonstrate how to include pieces of code, figures, and nested challenge blocks

::::::::::::::::::::::::::::::::::::::::::::::::
```


### Creating a New Episode

To add a new episode to a lesson,
we can run the `sandpaper::create_episode` function:

```r
sandpaper::create_episode("next-episode")
```

When you call this function, you should see a new file appear in the
`episodes` folder.
It will have the same example content as `01-introduction.Rmd` but 
with a different title in the YAML header, based on the name you specified
for the new episode in the call to `create_episode`.

## Previewing the Lesson

To see how the lesson website looks with this new episode added,
we can build and serve a local version of the site, which will be automatically
updated whenever we make changes to the source files.

```R
sandpaper::serve()
```

After a short wait, a preview of the built lesson site should pop into the _Viewer_
panel of RStudio. 
(You can "pop" it out into a web browser tab by clicking the little
_Show in new window_ button near the top of the Viewer panel.)

## Pushing to GitHub

push new episode back to github

## Editing an Episode

We will use the code block and output below to demonstrate one of the new features
provided by The Carpentries Workbench: automated feedback about changes to the
rendered lesson content that would be made by a pull request.

````markdown
```{r pyramid, fig.alt = "pie chart illusion of a pyramid", fig.cap = "Sun arise each and every morning"}
pie(
  c(Sky = 78, "Sunny side of pyramid" = 17, "Shady side of pyramid" = 5), 
  init.angle = 315, 
  col = c("deepskyblue", "yellow", "yellow3"), 
  border = FALSE
)
```
````

::: challenge

#### Change the colour of the pyramid

Following along with the workshop leads,
and working in RStudio on the local copy of your repository,
follow these steps:

1. Create a new branch in Git, and switch to it
1. Find the code block above in the new episode file that you created earlier.
1. Change the colours of the pyramid parts of the figure above 
   (defined in the `col` parameter of `pie`). 
   Here is a [resource for the available colour names in R](https://r-charts.com/colors/)
1. Commit the change
1. Push the branch to your remote repository on GitHub
1. Open a pull request to merge that branch into the `main` branch of your repository
1. Look at the preview of the changes to rendered content. 
   This should appear as a comment in the pull request discussion tab 
   shortly after the PR has been opened.

:::::: solution

````markdown

```{r pyramid-green, fig.alt = "pie chart illusion of a pyramid", fig.cap = "Sun arise each and every morning"}
pie(
  c(Sky = 78, "Sunny side of pyramid" = 17, "Shady side of pyramid" = 5), 
  init.angle = 315, 
  col = c("deepskyblue", "palegreen", "limegreen"), 
  border = FALSE
)
```
````

::::::
:::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Lesson sites are built from source repositories with GitHub Pages.
- A new lesson repository can be created from a template maintained by The Carpentries, and configured by adjusting the `config.yaml` file.
- The main pages of a lesson website are created from Markdown or RMarkdown files in the `episodes` folder.
- A local version of a lesson can be built and viewed with `sandpaper::serve()`.

::::::::::::::::::::::::::::::::::::::::::::::::::


[dc-home]: https://datacarpentry.org/
[GitHub]: https://github.com/
[Jekyll]: https://jekyllrb.com/
[lc-home]: https://librarycarpentry.org/
[md-template]: https://github.com/carpentries/workbench-template-md/generate
[R]: https://www.r-project.org/
[rmd-template]: https://github.com/carpentries/workbench-template-rmd/generate
[rmd-template-generate]: https://github.com/carpentries/workbench-template-rmd/generate
[styles-contributors]: https://github.com/carpentries/styles/graphs/contributors
[swc-home]: https://software-carpentry.org/
[YAML]: https://yaml.org/
[set-config](https://carpentries.github.io/sandpaper/reference/set_config.html#default-keypairs-known-by-sandpaper)

