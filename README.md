* Create an HTTP server with just nc
  * Basic response to test connectivity
    ```  
    while true; do { echo -e "HTTP/1.1 200 OK\r\n$(date)\r\n\r\n<h1>hello world from $(hostname) on $(date)</h1>" |  nc -vl 8082; } done
    ```
  * Return a file
     ```
     while :; do { echo -ne "HTTP/1.0 200 OK\r\nContent-Length: $(wc -c <some.file)\r\n\r\n"; cat ; } | nc -l 8080; done
     ```
* Test connectivity with a server with tools like NC, curl etc.
  * Below command works on linux servers only, need to test on containers. If connection would be successful you will get not response, if unsuccessful you will get Connection Refused error.
    ```
    echo "HEAD / HTTP/1.0" >/dev/tcp/localhost/8000
    echo "HEAD / HTTP/1.0" >/dev/tcp/<server>/<port>
    ```


