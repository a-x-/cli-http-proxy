<img width="300" src="https://cloud.githubusercontent.com/assets/6201068/16714438/4b0eaf94-46d4-11e6-8601-1acafc8acb3f.png" align="right"/>
# cli-http-proxy
Ultra simple CLI HTTP-proxy

## Using
`FROM_PORT=8081 TO_PORT=8080 ./run-proxy`

`open http://server:8080/`

### Long running setup
`FROM_PORT=8081 TO_PORT=8080 forever start /path/to/run-proxy`

`forever` already ships with the `cli-http-proxy`.

### Use case: http proxy from laptop (your own [ngrok](https://ngrok.com))

Ok, you have your own (or company's) server and laptop under firewall,

you want show web page from laptop.

`ngrok` migth be too slow or too public for you.

`ssh` + `cli-http-proxy` is the solution for you. Just do:

![term](https://cloud.githubusercontent.com/assets/6201068/16714487/c9142d00-46d5-11e6-9015-6d26d9f0a53a.png)

* **laptop**: `ssh -N user@server -R 8080:localhost:8081`
* **server**: `FROM_PORT=8081 TO_PORT=8080 ./run-proxy`

**scheme**:

```
                                          |
         <----------> localhost:8080 <--------> server:8081 <--------> server:8080
(   local server  )                  ( :22 ssh )         ( cli-http-proxy )
(e.g. node express)                       |
```


