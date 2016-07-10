<img width="300" src="https://cloud.githubusercontent.com/assets/6201068/16714438/4b0eaf94-46d4-11e6-8601-1acafc8acb3f.png" align="right"/>
# cli-http-proxy
Ultra simple CLI HTTP-proxy

## Instalation
`npm i cli-http-proxy`

## Using
```sh
FROM_PORT=8081 TO_PORT=8080 ./run-proxy`
open http://server:8080/
```

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

----

#### A lot of comprehensive schemes for novices
<details>
<summary>Click to unfold</summary>

**forwarding scheme**:

```
laptop                           your public server
  ( ) --------------------------------> ( )
                ( looks up )         
  ( ) <-------------------------------- ( )
                ( responds )
  ( ) <-------------------------------> ( )
        ( middlwares stores connection )
```

**tunnel scheme**:

```
laptop                                                                 server
                                          |
         <----------> localhost:8080 <--------> server:8081 <--------> server:8080
(   local server  )                  ( :22 ssh )         ( cli-http-proxy )
(e.g. node express)                       |
```

**networking scheme**:

```
laptop web server <------> ssh <------> server web proxy <------> user web client
```

![proxy](https://cloud.githubusercontent.com/assets/6201068/16714602/8b52daee-46d9-11e6-9dea-4ea32db51806.png)

</details>
