It's important to note that running this reset will drop any existing data you have in the application

heroku login                      => Firstly login heroku with this command to run on terminal
heroku run rails c --app app_name => to open rails oncole on heroku run this one command
heroku logs --app appname -t      => to check rails logs with tails run this command

To export the data from your Heroku Postgres database, create a new backup and download it.

heroku pg:backups:capture -a app-name
heroku pg:backups:download -a app-name

Now restore dump into local

pg_restore -U algo -h localhost -d protekt_lms_admin_development < /home/algo/projects/Protekt.LMS.Admin/latest.dump

How to reset PG Database on Heroku?
Step 1: heroku restart
Step 2: heroku pg:reset DATABASE (no need to change the DATABASE)
Step 3: heroku run rake db:migrate
Step 4: heroku run rake db:seed (if you have seed)
One liner

heroku restart; heroku pg:reset DATABASE --confirm APP-NAME; heroku run rake db:migrate

Note 1

Heroku doesn't allow users from using rake db:reset, rake db:drop and rake db:create command. They only allow heroku pg:reset and rake db:migrate commands.

More info: https://devcenter.heroku.com/articles/rake

Note 2

If you have more than 1 remote, append --remote [your_remote_name] like this:

heroku run rake db:migrate --remote dev (dev is example remote here)
