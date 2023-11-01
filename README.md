# sample-site

### Register new subdomain
Go to https://ecngx256.inmotionhosting.com:2083 to access the hosting platform
Sign in with the following credentials:

	username: creat750
	password: wJwn"8P>bc/D<@EL

Go down to Domains and select "Zone Editor"
Select "Manage" for the crclcrclcrcl.org domain
Here, add a CNAME record by clicking "Add a Record" and making the type "CNAME"
Make the name the subdomain you want, for example "xyz.crclcrclcrcl.org" and change the Record to crcl-epfl.github.io (assuming you are publishing your site from a repo in the CRCL EPFL organization)

### Installing Jekyll
Jekyll is a static site generator which reads Markdown files to create styled blog-type sites
This means that the themes and pages are usually structured around "posts" but there are ways to work around this to just make a more straightforward website
It's integrated with Github Pages, which allows you to set up a site at a custom domain quickly and without worrying about hosting

You first need to install `Ruby` and then you can install `Jekyll` and a handy utility called `Bundler`. Detailed instructions for this are here:
https://jekyllrb.com/docs/installation/

### Making a local site
Once installed you can run  `jekyll new mynewsite` to make a new site at `./mynewsite`, you can name this whatever you would like! If you go into the newly created directory, you can build the site locally with `bundle exec jekyll serve`.
If successful, the terminal message should say that you can view the site at http://127.0.0.1:4000/ or localhost:4000 in your web browser

### Customizing your site
The best way to make changes is to develop locally before publishing. Open the site directory in a text editor and any changes you make to the files (with the exception of a few core files) will be reflected in real time
#### Styling
The default theme is stored in a different directory from the site, so you will need to find the relevant files for the theme and place them in the site directory with the same name

To find the theme, you can run `bundle info --path THEME-NAME`

There are a few decent themes that work with minimal configuration between Jekyll and GH pages, listed [here](https://pages.github.com/themes/)
You can also find many more [here](https://jekyllthemes.io/free), but they will probably take some more work to get running
#### To get a GH Pages theme working
There are two files you need to change: `_config.yml` and `Gemfile`

In `_config.yml`, add `jekyll-remote-theme` to the plugins list, and change the theme name above it to the name specified in the repository documentation of the theme
Additionally, add a `repository` field, as many themes will look for this when building and throw errors if it's not there. This is usually referenced to make links to the repository in the site

Then, in order to view this theme locally, you'll need to make a few changes in the Gemfile
- Under the group plugins, add `gem "jekyll-remote-theme", "~> 0.4.3"`
- Additionally, uncomment line 15 and comment out line 10
- Add `gem "webrick", "~> 1.8"`

Run `bundle install` to get the latest bundles added in the above files

Finally, make sure that the `.md` files match the ones in the theme repository to see the pages as shown in the sample sites. The key thing is to match the Front Matter to what the theme has so that it can reference styles correctly

##### Customizing a theme
To change the layout:
Can do the command listed above (`bundle info --path THEME-NAME`) to find where the relevant files (`.html` and `.css`) are installed locally, then copy them into your site directory
Can also reference the GH repo for the theme for the same files

To change styles:
If you'd like to add your own custom styles:

1. Create a file called `/assets/css/style.scss` in your site
2. Add the following content to the top of the file:
    ```css
    ---
    ---
    
    @import "{{ site.theme }}";
    ```
3. Add any custom CSS (or Sass, including imports) you'd like immediately after the `@import` line

### Adding content
The GH pages themes do a great job of showing how MD is translated to a site page. You want to primarily work in the `index.md` page, which takes on the `default.html` layout 

### Publishing via GH Pages
You can either choose to make your site files as part of a project repository or as a separate repo
Once you have it running locally, all you need to do is add a [[custom workflow]] as a `.yml` file under a new folder `.github/workflows`
This ensures that the proper Gems are installed when Github builds the site
Lastly, make sure that in the `Settings` page for your repository under `Pages` that the `Custom Domain` points to your site