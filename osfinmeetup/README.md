1. php-nordic 
1.1 Load: for ((i=1;i<=10000;i++)); do   curl --header "Connection: keep-alive" "http://app.example.com"; echo ''; sleep 1;  done
2. Scale up
3. New build -> v.2

Blue/Green Deployment

1. php-nordic-nr -> name version1
1.1 for ((i=1;i<=10000;i++)); do   curl --header "Connection: keep-alive" "http://bg.example.com"; echo ''; sleep 1;  done

2. route
3. php-nordic-nr -> name version2
4. route change to version2
5. route change back

A/B Deployment
1. php-nordic-nr -> name version-1, no route
 - label prodmember=true
 
2. new service
 - oc expose dc/version1 --name=prod-service --selector=prodmember=true --generator=service/v1
 - oc expose service --name=prod-service --hostname=prod.example.com
2.1 for ((i=1;i<=10000;i++)); do   curl --header "Connection: keep-alive" "http://prod.example.com"; echo ''; sleep 1;  done
3. update code
4. new app with label prodmember=true 
