# chaosma.github.io

### Deployment

manually deployment:

1. Generate x509 certificate:
   openssl req -newkey rsa:2048 -nodes -keyout threelifestone.com.key -x509 -days 365 -out threelifestone.com.crt
   sudo cp threelifestone.com.crt /etc/ssl/certs/
   sudo cp threelifestone.com.key /etc/ssl/private/

2. configure nginx:
   see threelifestone.com.conf

3. create http and https versions and put into /var/www/http and /var/www/https separately

- (http) jekyll serve --host=threelifestone.com --port=80
- (https) jekyll serve --host=threelifestone.com --port=443 --ssl-cert threelifestone.com.crt --ssl-key threelifestone.com.key


