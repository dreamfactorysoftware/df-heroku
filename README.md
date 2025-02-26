# Heroku Buildpack for DreamFactory

This is a Heroku buildpack for [DreamFactory](https://github.com/dreamfactorysoftware/dreamfactory), an open-source REST API backend platform.

## Usage

### Create a new Heroku app with this buildpack

```bash
# Create a new Heroku app
heroku create myapp

# Set the buildpack
heroku buildpacks:add heroku/php -a myapp
heroku buildpacks:add https://github.com/dreamfactorysoftware/df-heroku.git -a myapp
```

### Add to an existing Heroku app

```bash
heroku buildpacks:add heroku/php -a myapp
heroku buildpacks:add https://github.com/dreamfactorysoftware/df-heroku.git -a myapp
```

Note: This buildpack requires the official Heroku PHP buildpack to be added first.

### Required Configuration

Set the following environment variables in your Heroku app:

```bash
# Database configuration
heroku config:set DB_CONNECTION=pgsql -a myapp
# If using Heroku Postgres, these will be set automatically
# Otherwise, set them manually:
# heroku config:set DB_HOST=your-database-host -a myapp
# heroku config:set DB_PORT=5432 -a myapp
# heroku config:set DB_DATABASE=your-database-name -a myapp
# heroku config:set DB_USERNAME=your-database-user -a myapp
# heroku config:set DB_PASSWORD=your-database-password -a myapp

# Application configuration
heroku config:set APP_ENV=production -a myapp
heroku config:set APP_DEBUG=false -a myapp
heroku config:set APP_URL=https://your-app-name.herokuapp.com -a myapp
```

### Database Setup

This buildpack supports PostgreSQL by default. To add a PostgreSQL database to your Heroku app:

```bash
heroku addons:create heroku-postgresql:hobby-dev -a myapp
```

### Deployment

You can deploy DreamFactory to Heroku in two ways:

1. **Deploy from an existing DreamFactory repository**:
   ```bash
   # Clone the DreamFactory repository
   git clone https://github.com/dreamfactorysoftware/dreamfactory.git
   cd dreamfactory
   
   # Create a Heroku app and set buildpacks
   heroku create myapp
   heroku buildpacks:add heroku/php -a myapp
   heroku buildpacks:add https://github.com/dreamfactorysoftware/df-heroku.git -a myapp
   
   # Set up database
   heroku addons:create heroku-postgresql:hobby-dev -a myapp
   
   # Deploy
   git push heroku main
   ```

2. **Deploy a new app with the buildpack**:
   ```bash
   # Create a new directory
   mkdir my-dreamfactory-app
   cd my-dreamfactory-app
   
   # Initialize git
   git init
   touch README.md
   git add README.md
   git commit -m "Initial commit"
   
   # Create a Heroku app and set buildpacks
   heroku create myapp
   heroku buildpacks:add heroku/php -a myapp
   heroku buildpacks:add https://github.com/dreamfactorysoftware/df-heroku.git -a myapp
   
   # Set up database
   heroku addons:create heroku-postgresql:hobby-dev -a myapp
   
   # Deploy
   git push heroku main
   ```

## Features

- Automatic installation of DreamFactory
- Integration with Heroku's PHP buildpack for PHP dependencies
- Automatic database migrations
- Proper file permissions setup
- Post-deployment configuration

## Support

For issues with this buildpack, please file an issue on the GitHub repository.
For DreamFactory-specific issues, please refer to the [DreamFactory documentation](https://guide.dreamfactory.com/).

## License

This buildpack is released under the Apache 2.0 License. 