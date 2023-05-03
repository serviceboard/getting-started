# Getting started with Serviceboard
## Prerequisites
- bash
- docker
- docker-compose
- serviceboard docker images:
```bash
docker load --input backend-v1.0.0.tar.gz
docker load --input frontend-v1.0.0.tar.gz
```

## Configuration
- Create .env file (use example.env as template)
- Generate secret keys (once) and put them into .env
```bash
for secret in  SECRET_KEY_BASE JWT_SECRET_KEY SETTINGS_SECRET_KEY INTEGRATIONS_SECRET_KEY
do
 echo $secret=$(openssl rand -hex 64)
done
```

## Run
- DB initialization
```bash
docker compose run --rm db-init 
```
- Start Serviceboard
```bash
docker compose up  -d
```
Application should be available at http://localhost:8080 and API at http://localhost:3000/api/v1, default user/pass: admin/admin123

to change admin password start Rails console:
```bash
docker compose run backend bundle exec rails c
```
then run inside rails console
```ruby
User.find_by(uid: "admin", provider: "local").update(password: "new_password")
```