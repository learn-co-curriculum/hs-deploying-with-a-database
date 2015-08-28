## Get Ready to Deploy...

Our applications have been using sqlite3 in development, but to deploy to Heroku we'll need to use Postgres, a different flavor of SQL. Luckily, ActiveRecord will automatically use the correct SQL syntax with some basic configuration. 

### Gemfile - Add the `pg` gem to your gemfile. 

```ruby 
  gem 'pg'
```

Run bundle install. If you get an error, you may need to install Postgres on your system. Copy the following code into your terminal: `sudo apt-get install postgresql`

### environment.rb  - Setup an ActiveRecord Connection
In the config directory. 

```ruby
configure :development do
  set :database, "sqlite3:db/database.db"
end

configure :production do
  ActiveRecord::Base.establish_connection(ENV["DATABASE_URL"])
end
```

This sets up a connection to the database we will for production separately from our development database.


### Get Heroku Ready

Lastly, we need to add a database to our heroku app. We can do this from the command line by running `heroku addons:create heroku-postgresql:hobby-dev`. This will create a postgres database for your heroku app. 

### Push Your Changes

Remember to add, commit, and push your changes to github and heroku. Sit back, relax OR google your error!

### Common Bugs

+ We only have `pry` in our development group, so make sure it's not required in your application controller before you push to heroku. 
