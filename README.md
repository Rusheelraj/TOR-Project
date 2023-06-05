# Hosting and analysis of TOR network 
This is a team project (2) which we worked on hosting and analysing the TOR network during my Masters second semester. 

## ---------------------- Anonymising network traffic using Proxychains -----------------------

Step - 1 : Installing proxychains:

``` $ sudo apt install proxychains ```

``` $ sudo apt install proxychains4 ```

Step - 2: Configuration of proxychains:
Navigate to the /etc folder and open the proxychains4.conf file to edit the configuration changes. Uncomment the type of chaining needed for the proxychains. In our case, we want to test it on dynamic chains.

#dynamic_chain -> dynamic_chain

``` socks5 127.0.0.1 9050 ```

Step - 3: Once the configuration changes are done, open a new terminal window and start the proxchains with a web-browser as well as a website we want to connect.

``` $ proxychains4 firefox whatismyipaddress.com ```

![image](https://github.com/Rusheelraj/TOR-Project/assets/30828807/d4fb5b43-440b-4d14-ba8d-214b530f450b)

Step - 4: This is how we can view the proxychains traffic in the terminal. We can notice that the type of chain used in this connection is “Dynamic Chain”, localhost 127.0.0.1 and port 9050 with resulted IP address which we wanted to search. The last column describes the HTTP status code of the http request.

![image](https://github.com/Rusheelraj/TOR-Project/assets/30828807/8fa3bb91-53f9-43c5-8b35-9753cf10edfe)

Step – 5: Let us check whether the traffic is really anonymizing. Online public IP address viewer can help us find out. Once the proxychains is established, we can see that our public IP is completely anonymized. The IP address is at location “Iceland” with a IP address as “89.147.110.214”

Check the IP address.

![image](https://github.com/Rusheelraj/TOR-Project/assets/30828807/d368ce2a-d778-4cd0-94c0-36634aa6c67e)

Step – 6: Let us also check DNS leak test. A DNS leak test is a tool that determines whether a user's DNS requests are being leaked or exposed outside of an encrypted VPN or proxy tunnel.

When a user visits a website or other online resource, their device sends a DNS request in order to translate the domain name into an IP address. If the DNS request is not delivered through the encrypted tunnel, the user's Internet Service Provider (ISP) can track their online activities and potentially identify their location and identity. DNS leak testing operates by mimicking DNS requests from the user's device and determining whether they are routed through the encrypted tunnel or are leaked outside of it. The test usually entails contacting a website or service that displays the user's IP address and comparing it to the IP address of the VPN or proxy server to which they are connected.

DNS leaks can occur as a result of incorrectly configured VPN or proxy settings, network connectivity problems, or software defects. DNS leak tests are useful because they assist users in identifying and correcting potential privacy and security issues, as well as selecting VPN or proxy services that do not leak DNS requests.

![image](https://github.com/Rusheelraj/TOR-Project/assets/30828807/18613c1c-58d4-45a9-b9ac-e038f8ffbb2c)

## ---------------------------------- Hosting a TOR onion website ----------------------------------

Step - 1: Open a terminal window on Kali Linux Install Tor by running the following command:

``` $ sudo apt-get install tor ```

Once Tor is installed, we can check its status by running the following command:
``` $ sudo service tor status ```

To automatically launch Tor when Kali Linux starts up, we can add the following command in our system's startup programs:
``` $ sudo systemctl enable tor.service ```

This will add the Tor service to the list of services that start up when Kali Linux boots. Also, we can start the Tor service manually by running the following command:
``` $ sudo systemctl start tor.service ```

Once the service is started, we can use the Tor browser to access .onion sites and browse the web anonymously.

Step - 2: Traverse to /var/lib/tor/hidden_service and uncomment the two lines present in the location-hidden services. 

HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 80 127.0.0.1:8080 // Here, we are binding the port 8080

![image](https://github.com/Rusheelraj/TOR-Project/assets/30828807/76f0bfc9-922a-40ad-93d4-ad10115b9539)

Step – 3: Start the TOR service. This can be performed just by a simple command.
``` $ sudo service tor start  ```

``` $ sudo service tor status ```

![image](https://github.com/Rusheelraj/TOR-Project/assets/30828807/42b322da-eb12-429c-9de6-1f746ecfeb28)

Step – 4: Start running the in-built python’s HTTP server and bind the IP and port with HTTP server. This can be performed by the command.

``` $ sudo python3 -m http.server –bind 127.0.0.1 8080 ```

![image](https://github.com/Rusheelraj/TOR-Project/assets/30828807/0d41d2c6-a63f-465f-966b-34194a07dedf)

Step - 5: But we must have an address to access the site. This can be found in /var/lib/tor/hidden_service folder. Open the hostname by using the “cat” command.
Traverse to this path! 

``` $ cd /var/lib/tor/hidden_service  ```

There is a file called "hostname". This is where the TOR stores the URL name for your hidden website service. 

![image](https://github.com/Rusheelraj/TOR-Project/assets/30828807/8527b1bf-3733-4f8c-a6ef-f32a8b4d4d84)

Step – 6: Download the executable file of TOR browser from the official website and run it. 
![image](https://github.com/Rusheelraj/TOR-Project/assets/30828807/df278c9a-5fdd-4da9-8ee3-a7aae5b8b9f1)

Type in this URL onto the TOR browser.
zq7yfndhqwoqvmkujfvphddracckd53da3mrjplb7y5w7puacedjt2yd.onion

Once, we type in the URL (.onion site) in TOR browser, it automatically connects to the TOR network and accesses the .onion sites anywhere in the world. 
The below image is the result of the hosted website on TOR.

![image](https://github.com/Rusheelraj/TOR-Project/assets/30828807/e6c544a7-2116-4129-9591-8158d2e1ceab)

