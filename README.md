Reservasi Backend for Laboratorium Pemrograman I Teknik Informatika ITS Surabaya, Indonesia
================
### How To Deploy
1. Remember to update & install dependency before deploy
```sh
$ bundle update
$ bundle install
```

2. Copy config/local_env.yml.example to config/local_env.yml and edit with your configuration in  your environment (Dev/Prod). 

## Dev
* rails s -b 0.0.0.0 -p 10003 -d

## Prod
* To create devise secret key, using
```sh
$ bundle exec rake secret 
```
* Create server key, using 
```sh
$ RAILS_ENV=production rails secret
```
Put both key in config/local_env.yml
* rails s -b 0.0.0.0 -p 10003 -d -e production
* OR `nohup rails s -b 0.0.0.0 -p 10003 -d -e production`
* OR `tail -f nohup.out` if u want to read log.
--------

* Ruby & Rails version
    - ruby 2.3.1p112 (2016-04-26 revision 54768) [x86_64-linux]
    - Rails 5.1.5
* System dependencies
  - Ubuntu 16.04 (Prod), Ubuntu Mate 16.04(Dev)
  - MySQL (Dev & Prod)
  - Puma (Dev & Prod)
* Configuration
  - Setting u'r DDoS params (im 2 lazy 2 write right now)
    - http://sourcey.com/building-the-prefect-rails-5-api-only-app/
* Database creation  
    - rails db:create
* Database initialization
    - rails db:migrate
* Deployment instructions
  - Bundle install
  - Create Admin Account using ruby command (in root web dir)
    - rails c
    - rails > User.create(email:'a@a.com', password:'changeme', password_confirmation:'changeme')
    - Do POST data, for getting token, ex
        - curl -X POST -d email="a@a.com" -d password="changeme" http://localhost:3000/auth_user
        - Response :
            - {"auth_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxfQ.po9twTrX99V7XgAk5mVskkiq8aa0lpYOue62ehubRY4","user":{"id":1,"email":"a@a.com"}}
    - After getting token, threw it in header
        - curl --header "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxfQ.po9twTrX99V7XgAk5mVskkiq8aa0lpYOue62ehubRY4" http://localhost:3000/home
  - Run : rails s
    - binding : -b. Example : rails s -b 0.0.0.0
    - port(default:3000) : -p 8080. Example: rails s -p 8080
    - run on background : -d. Example: rails s -d
* Auth
  - Iam Using JWT, from https://www.sitepoint.com/introduction-to-using-jwt-in-rails/
