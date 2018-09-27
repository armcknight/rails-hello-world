# rails-hello-world

A simple “Hello world!” [Rails](https://rubyonrails.org) app with a PostreSQL database that works with [`rbenv`](https://github.com/rbenv/rbenv).

## Create from scratch

```sh
# make sure we have rails
rbenv exec gem install rails --no-ri --no-doc

# create new rails app
rbenv exec rails new myapp --database=postgresql --skip-bundle --skip-git # we'll bundle ourselves after configuring how to do it, and don't let rails create its own Git repo–that's up to you!

pushd myapp

# install/package dependencies declared by rails in Gemfile
rbenv exec bundle package --path=vendor/bundle

# create the “Hello world!” view/controller
rbenv exec bundle exec rails generate controller welcome # we're now bundle exec'ing rails because it was installed via the Gemfile created with rails new ...
echo "<h2>Hello World!</h2>" > app/views/welcome/index.html.erb

# add route to welcome app's index
sed -i '' 's/end/  root \'welcome#index\'\
end/g' config/routes.rb

# add a Procfile for Heroku
echo "web: rails server
local: rbenv exec bundle exec rails server" > Procfile

popd
```

## Deployment

### Local

```sh
pushd myapp
rbenv exec bundle exec rails server &
open http://localhost:3000
popd
```

### Locally with Heroku

```sh
pushd myapp
heroku local local &
open http://localhost:5000
popd
```

## Remote

### Heroku

```sh
heroku create # make sure your ‘heroku’ git remote points to the correct app's git url, like if there was a previous one
git push heroku master
open $HEROKU_RAILS_URL
```

## References

- [Getting Started on Heroku with Rails 5.x](https://devcenter.heroku.com/articles/getting-started-with-rails5#create-a-new-rails-app-or-upgrade-an-existing-one)

> Note: References preserved as PDFs in `docs/`.

