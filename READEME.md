for working with docker compose and nginx web server

Create repo with gh command
gh auth login # -> web, token 
# token -> permission 3 ( repo , org , admin:org)
gh auth status # show the status of auth 

gh repo create dockercomposenginxessentials --public
gh repo view dockercomposenginxessentials --json sshUrl | jq -r '.sshUrl'
gh repo view dockercomposenginxessentials --json url | jq -r '.url'

git init 
git remote add origin $(gh repo view dockercomposenginxessentials --json url | jq -r '.url'
)

git remote -v # show origin of the project 


+++++++++++++++++++++++++++++

-- docker compose up  service_name -d  // up container with specify service_name 

--  


# Checking serivces

curl http://localhost:9999

# checking with ip 

curl http://localhost:192.168.0.2

# using Apache to testing Least Connection Load Balancing
sudo apt update 
sudo apt install apache2-utils -y 
ab 

ab -n [number of requests] -c [concurrent requests] http://[hostname]/
                                // access to load balancing port
ab -n 1000 -c 10 http://localhost:8888/
