<h1 align="center">Reflection</h1><h4 align="center">The Automated Parameter Finder &<br>XSS/SQLi/SSRF tester</h4>

## About

Reflection was created with the main purpose to be fast and a reliable tool to add to your toolbox. It lets you find secret parameters and with this, quickly test for a potential **XSS** , **SQLI**, or **SSRF**. Reminder, while it can be a great tool and already proved itself with some great results, nothing is perfect and work was made to minimize false positives since the beginning so if you find an issue or have any ideas on how we can minimize this, even more, we would be more then happy to take a look :)

![Flag 1 - Recon](/tool.gif)
<img align="center" src="https://i.ibb.co/Yf0bw1c/sshhhhhh.png">



## Installation

The installation is very easy, all you have to do is:

```
git clone https://github.com/mikey96/reflection-public.git
cd reflection-public
pip3 install -r requirements.txt
```



## Usage

Reflection can use **Discord Webhooks** to return the output to the users. If you want to know how to create a web-hook on discord you can follow [this tutorial](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks). These are the available  flags on Reflection:

```
Required Flags:

  1. -e | List containing endpoints  | Ex. python3 reflection.py -e endpoints.txt
    - Endpoint Example - https://victim.com/ or https://victim.com/something.php
  2. -p | List containing parameters | Ex. python3 reflection.py -p params.txt
  3. -o | Outputs scan results       | Ex. python3 reflection.py -o scan_results.txt

Optional Flags:
	
  1. -rec [on] | Recursive search of parameters and return all reflected | Ex. python3 reflection.py -rec on
  2. --mode [1 to 5] | Vulnerability Type Mode | Ex. python3 reflection.py --mode 4
	- Mode 0 - Reflection scan with GET endpoints (Default Option)
	- Mode 1 - Reflection scan with POST endpoints
	- Mode 2 - Reflection scan with GET and POST endpoints
	- Mode 3 - Reflection scan confirming XSS
	- Mode 4 - Reflection scan for SQLI vulnerabilities
	- Mode 5 - Reflection scan for SSRF vulnerabilities
        
  3. -t [NUMBER]          | Threads                           | Ex. python3 reflection.py -t 100
  4. --cookie [COOKIE]    | Settings Cookies                  | Ex. python3 reflection.py --cookie cookie_monster
  5. --discord [WEB_HOOK] | Setup Discord Web-Hook            | Ex. python3 reflection.py --discord https://WEB_HOOK.com
  6. -fp [PARAM1,PARAM2]  | Filters Out certain params        | Ex. python3 reflection.py -fp param1,param2
  7. -v [ON]              | Verbose for better output         | Ex. python3 reflection.py -v on
  8. -hi [FILENAME.txt]   | Hidden input names to an File     | Ex. python3 reflection.py -hi hidden_inputs.txt
  9. -bc [BURP-COLLAB]    | Burp Collaborator for SSRF Mode   | Ex. python3 reflection.py -bc http://burp_collab_link.net


```



#### Command for XSS Hunting

`python3 reflection.py -e endpoints.txt -p params.txt -o output.txt -rec on --mode 2 --discord [WEBHOOK_URL] -t 50`

#### Command for SQLI Hunting

`python3 reflection.py -e endpoints.txt -p params.txt -o output.txt --mode 4 --discord [WEBHOOK_URL] -t 50`

#### Command for SSRF Hunting

`python3 reflection.py -e endpoints.txt -p params.txt --mode 5 --bc [BURP COLLABORATOR] -t 50`



## Little Scrips to make your life easier

##### Burp Cleaner | Generate an endpoint list from burp proxy history file

1. You can collect additional parameters not present in your parameter list and write them to it using using  `-p [FILE_NAME.txt]`
2.  You can filter out specified filetypes using `-ft .[EXTENSION]`

`python3 tools/burp-cleaner.py -i history.xml -o history.txt -ft .js,.css,.rtf [-p params.txt]`



##### Httpx / Gau Cleaner | Generate an endpoint list from httpx /gau output file

1. You can collect additional parameters not present in your parameter list and write them to it using using  `-p [FILE_NAME.txt]`
2.  You can filter out specified filetypes using `-ft .[EXTENSION]`

`python3 tools/httpx-cleaner.py -i output.txt -o endpoints.txt -ft .js,.css,.rtf [-p params.txt]`



##### List Cleaner | Clean the newly generated list of reflected parameter URLs

`python3 tools/list-cleaner.py -i test.txt -o test-clean.txt`



## Thanks

Reflection was made by [Mikey](https://twitter.com/mikey96_bh) and [Castilho](https://twitter.com/castilho101).<br>We appreciate all the support and if you have any questions or feedback, don't hesitate to hit us up. 

Best regards, Mikey and Castilho.  
