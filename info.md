Info on data sources, repository and software details
========================================================

Data for Germany from Robert Koch Institute
----------------------------------------------------

-   From <https://npgeo-corona-npgeo-de.hub.arcgis.com/> -\> Menu top
    left -\> \"Data\", scroll down to \"RKI Corona Landkreise\" data
    set, -\> select interesting data set -\> for example
    -   RKI Corona Bundesländer
    -   RKI COVID19 -\> RKI Corona Landkreise
    -   Download button (below image, on the right) -\> Full Data set
        -\> Spreadsheet This provides a link to a csv file, but with a
        URL that includes a hash. As of 9 April, this is
        <https://opendata.arcgis.com/datasets/ef4b445a53c1406892257fe63129a8ea_0.csv>


Overall set up of directory structure and software
==================================================

Directory structure for repository
<https://github.com/fangohr/coronavirus-2020>:

coronavirus-2020 (root dir of repository)
-----------------------------------------

contains `coronavirus.py` as the main file required to create the plots

-   notebooks will import from this or use %run to execute it
-   this is the authorative copy of coronavirus.py

Also contains `index.ipynb` and `germany.ipynb` as the initial way of
presenting the plots. They can probably be replaced by the static
webpages, or be used to show some particular interesting data sets.

Other files:

-   [info.md](info.md) : this file, provides overview of current setup
-   [todo.md](todo.md) : things that need doing (programming/software
    engineering/data analysis)
-   [ideas.md](ideas.md): things that could be done; might need some evaluation
    first

coronavirus-2020/tools
----------------------

contains tools to create static webpages at
<https://fangohr.github.io/coronavirus>, (repository to host webpages is
<https://github.com/fangohr/coronavirus-2020>)

in particular:

-   generate-countries.ipynb Notebook that creates all the static
    wepages for the world, and Germany

-   template-country.ipynb (used for world countries)
-   template-germany.ipynb (used for Germany)

Hack: to run `generate-countries.ipynb` we copy at the beginning, the
`coronavirus.py` file from the parent directory. Important to remember
that the authorative file is in the parent directory.

coronavirus-2020/tools/wwwroot
------------------------------

-   rootdirectory of <https://fangohr.github.io/coronavirus> and
    repository

-   files that are added to the repository
    <https://github.com/fangohr/coronavirus-2020>, and then pushed, will
    show up at <https://fangohr.github.io/coronavirus> a few minutes
    later

-   we use a separate repository (I.e. different from code repo) out of
    fear that it may grow quickly in size. At that point, we can create
    a new repository under the same name, as the history is pretty
    irrelevant: this is only to serve the most recent data in static
    html files.

-   The total size of html file for world and Germany is around 300MB,
    but the .git directory is smaller.

-   The files committed to the webpages repository must contain the most
    recent `coronavirus.py` and `requirements.txt` as those are needed
    by binder to execute the notebooks.

-   By also commiting the `cachedir`, people don\'t need to re-fetch the
    data on the binder service (fetching of the German data set varies
    between 1s and 60 seconds).


coronavirus-2020/tools/pelican
-----------------------------------

Base directory of Pelican (static html generator) package.

- run `make html` here to create html in `../wwwroot`. Use this for development. 
- run `make publish` here to create html that is meant to be pushed to the website:
  - `make publish` executes the settings is `publishconf.py` after having executed `pelicanconf.py`.
    As such, we get absolute URL in feeds, we  get feeds with links to new articles. It also adds
    the google analytics tracker that we don't want for development, and javascript to enable disqus.
    (Not sure if we want the latter, but we might as well set it up while there is no traffic on the page,
    and then deactivate if we don't want it.)

- the `generate-countries.ipynb` notebook creates files `germany.md` and `world.md` in pelican/contents

- `tools/pelican/contents`:
  - keeps markdown or rstfiles that pelican will turn into articles automatically 
  
- `tools/pelican/contents/pages`:
  - keeps static files (such as the welcome page), will also be turned to html

coronavirus-2020/archive
------------------------

-   files for history interest - can be removed soon. There were
    initially interesting to look up some things tried before.

coronavirus-2020/dev
--------------------

1. clone git@github.com:fangohr/coronavirus-2020.git into your chose directory
   X. This provides the source code.

2. Get the repository that keeps the static webpages (using github pages)

"cd tools && git clone git@github.com:oscovida/oscovida.github.io.git wwwroot"

Procedure to update data and webpages
==============================================

3. update notebooks by running (in X/tools)

   jupyter-notebook generate-countries.html 
   
4. in X/tools/pelican, run ``make html` to update html pages (to develop), `make
   publish` for the final version

5. in `wwwroot`, run `git add *; git commit *`, then `git push`

6. updates should appear at https://oscovida.github.io a few minutes later





Related resources
=================

-   <https://nextstrain.org/ncov>
-   Jupyter notebooks as templates: <https://covid19dashboards.com/> One
    of these is
    -   <https://covid19dashboards.com/compare-country-death-trajectories/>
        -   nice comparison of trajectories
            -   would be good to have per state or \'Landkreis\'
