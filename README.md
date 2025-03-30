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
  * [Reverse shells in bash](https://hypothetical.me/post/reverse-shell-in-bash/)
  * [TCP connections in ZSH ->](https://hypothetical.me/post/zsh-tcp/)
 
*  Rsync command to transfer file from local to server
  *
    ```
    rsync -avz <file-name> username@remote-server:/home/ubuntu
    ```
  * ```
    rsync -avz -e "ssh -i /path/to/private_key" /path/to/local/file username@remote-server:/path/to/remote/destination
    ```
 * Linux get output of the last command (print 1 if failure and 0 if last command was success)
     ```
      echo $?
     ```
 * Postman scripts
   ```
   option1:
     var jsonData = JSON.parse(responseBody);
     postman.setEnvironmentVariable("authToken", jsonData.token);

   option2:
     let responseData = pm.response.json();
     let orgId = responseData.data.org_id;
     pm.collectionVariables.set("org_id", orgId);
   ```
  * kubernetes alias
    ```
    alias klogst=kubectl logs -f --tail=30
    # kubernetes admin token
    alias kat=kubectl -n kubernetes-dashboard create token admin-user | pbcopy
    ```
 * Decode base64 cert and describe it
    ```
    alias decodecert="pbpaste | base64 --decode > ~/Downloads/temp.crt && openssl x509 -in ~/Downloads/temp.crt -noout -text; rm -rf ~/Downloads/temp.crt"
    alias cert="pbpaste > ~/Downloads/temp.crt && openssl x509 -in ~/Downloads/temp.crt -noout -text; rm -rf ~/Downloads/temp.crt"
    ```
 * convert RSA key to normal key
    ```
    openssl pkcs8 -topk8 -inform PEM -outform PEM -in key-file-name.txt -out output-key-file-name.txt -nocrypt
    ```
 * bash to execute remote script
    ```
    bash <(curl -k "https://s3.aws.com/deploy.sh") argument1 argument2
    ```
 * Kubernetes required images
    * kubeadm config images list
        <img width="772" alt="image" src="https://github.com/user-attachments/assets/20033baa-093e-4275-aecf-da05ea8f4cc0" />
    

