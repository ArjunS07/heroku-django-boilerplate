# Heroku Django boilerplate
This git repository is meant to be a bare-bones template for creating Django apps that can quickly be deployed to Heroku.

## Template information

### Packages
This template uses pipenv and contains the following packages:
* django
* gunicorn
* dj-database-url
* psycopg2-binary
* whitenoise
* django-environ

### Settings configuration
* The secret key is ready to be configured from a local .env file and Heroku variables
* dj-database-url is used for configuring the database URL
* Static files are configured. urls.py also contains a static URL
* Sentry placeholder configuration for logging errors in production

## Install instructions
### Prerequisites
You need to have the following installed on your system:
* Python
* Pipenv
* Heroku CLI

### Preparing for deployment
1. Clone this repository:
`git clone TODO`

2. Navigate into the template folder
`cd template`

3. Install dependencies from the Pipfile
`pipenv install`

4. Activate the pipenv virtual environment
`pipenv shell`

5. Update your environment variables in your `.env` file:
    1. Run `echo "SECRET_KEY=$(openssl rand -base64 32)" > .env` in the same directory as the `.env` file
    2. Open the file and set `DEBUG=True` in a new line

6. Test the local django server
`python manage.py runserver`

7. Rename the project:
a. Run @[FredPerr](github.com/FredPerr)'s [script](https://github.com/FredPerr/django_super/blob/main/rename-project.py) (also included in this project) to rename most instances of the project name.
`python rename-project.py PROJECT_NAME`
b. Manually rename the the `heroku_django_boilerplate` root folder

8. Update the `Procfile`:
`web: gunicorn PROJECT_NAME.wsgi`

9. Update your secret key
`echo "SECRET_KEY=$(openssl rand -base64 32)" > .env`

10. Test the local heroku server
`heroku local` or `heroku local web`

### Deployment
1. Commit your changes
2. Create a heroku app for this project:
`heroku create`.
You can optionally pass in a unique project name after this command
`heroku create myuniqueappname`
3. Update your environment variables on the Heroku server:
    1. Run `heroku config:set SECRET_KEY='YOURRANDOMSECRETKEY'`, using the value that was previously autogenerated and inserted into your .env file
    2. Run `heroku config:set DEBUG=False` 
4. (optional) Check the remotes for your repository. If a second remote for Heroku has not been added, run:
`heroku git:remote myuniqueappanem`
5. Push your code to the main/master branch
`git push heroku main` or `git push heroku master`

**Voila!** Open the URL heroku gives you when you run that command (or run `heroku open`) and you should be able to see your site. 