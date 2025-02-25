# Heroku Buildpack for DreamFactory

This is a Heroku buildpack for [DreamFactory](https://github.com/dreamfactorysoftware/dreamfactory), an open-source REST API backend platform.

## Usage

### Create a new Heroku app with this buildpack

```bash
# Create a new Heroku app
heroku create myapp

# Set the buildpack
heroku buildpacks:set https://github.com/yourusername/df-heroku-build.git -a myapp
```

### Add to an existing Heroku app

```bash
heroku buildpacks:set https://github.com/yourusername/df-heroku-build.git -a myapp
```

### Required Configuration

Set the following environment variables in your Heroku app:

```bash
# Database configuration
heroku config:set DB_CONNECTION=pgsql
heroku config:set DB_HOST=your-database-host
heroku config:set DB_PORT=5432
heroku config:set DB_DATABASE=your-database-name
heroku config:set DB_USERNAME=your-database-user
heroku config:set DB_PASSWORD=your-database-password

# Application configuration
heroku config:set APP_KEY=$(php artisan key:generate --show)
heroku config:set APP_ENV=production
heroku config:set APP_DEBUG=false
```

### Database Setup

This buildpack supports PostgreSQL by default. To add a PostgreSQL database to your Heroku app:

```bash
heroku addons:create heroku-postgresql:hobby-dev
```

## Features

- Automatic installation of PHP 8.1 and required extensions
- Composer dependency management
- Automatic database migrations
- Proper file permissions setup
- Cache configuration

## Support

For issues with this buildpack, please file an issue on the GitHub repository.
For DreamFactory-specific issues, please refer to the [DreamFactory documentation](https://guide.dreamfactory.com/).

## License

This buildpack is released under the Apache 2.0 License. 