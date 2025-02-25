# To run locally:
1. Run `bundle exec jekyll serve`
2. Go to http://localhost:4000/


# In progress projects
To change the projects in progress, add/remove to the `_in_progress` folder

To disable:
1. Move markdown files over into the `_portfolio` folder
2. Go to `_layouts/collection.html` and comment out the instructed portions

To enable:
1. Move markdown files over into the `_in_progress` folder
2. Go to `_layouts/collection.html` and uncomment out the instructed portions


# Add new plugins
1. Add to `Gemfile`
2. Run `bundle install`
3. Add plugin into the plugins section in `_config.yml`

# Resize GIFS
Use 360x240
