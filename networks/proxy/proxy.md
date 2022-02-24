# Proxy, Intranet & VPN

## Proxy

A `proxy server` is a server that **retrieves data from the Internet for a user**.

![img_1](/networks/proxy/resources/proxy_server.jpg)

The proxy server use a an in-betweener/a middleman between the user and the Internet. It listens for user requests and then proceeds to retrieve the data from the Internet. 

Proxy servers **cache web pages recently visited** so they do not have to query the same web page again and again. They already have main information so the connection speed is decreased. 
### Why do people use proxy servers ?

1. It increases speed because proxy server **cache web pages recently visited**.
2. It allows companies to monitor their employees' online activities.
3. It assures **privacy** because the user IP is hidden behind the proxy server. (see *RECAP*) 

## Intranet

An `Intranet` is a private, secure network used by employees for internal communication and information sharing within a company or organization.

![img_2](/networks/proxy/resources/extranet-internet-intranet.jpg)

Companies often let their employees connect to their servers only when they are inside their buildings. So, it is part of the Intranet and it is not possible to access their servers remotely. In fact, it is not possible unless you use a **VPN**.

## VPN (Virtual Private Network)

### Organizations

A `Virtual Private Network` encrypts the data that's being transferred over the Internet.

It provides a **dedicated secure tunnel between 2 points over the Internet**. Companies which have multiple sites/buildings, where one of the sites host databases/servers, often use a VPN in order to have their data accessible from each and every site. 

There are 2 types of VPN used by organizations:

| Site-to-Site                                                                                           | Remote Access                                                   |
|:-------------------------------------------------------------------------------------------------------|----------------------------------------------------------------:|
| connects 2 entire networks                                                                             | grant access to the corporate network but only for one device   |
| always active                                                                                          | not always active                                               |
| both networks need to be configured                                                                    | companies network and the used device needs to be configured    |
| perfect for companies that have several buildings and need to access servers in one of these buildings | perfect for employees who works remotely                        |


![img_3](/networks/proxy/resources/site2site&remote_acess.jpg)

### Public-oriented VPNs

Known VPNs companies (such as *Nord VPN, Express VPN...*) use other arguments to describe VPNs. They promote these points:

- It hides the user's IP address from the ISP (Internet Service Provider) and from the government. So, it can be used in countries where fondamental liberties are not granted.
It assures **privacy** and can be used to act as if we were in another country (Netflix, Ticket reservation)
- It is safer to browse the Internet with a VPN, especially if you are connected to a public access point. **As your data is encrypted from your computer until they arrived to the VPN provider's server, it cannot be intercepted by a potential hacker**.

A **public-oriented VPN** encrypts the user's data between his device and the VPN provider's server. Then, this server retrieves the desired web information with its own IP address.

![img_4](/networks/proxy/resources/common-vpn.jpg)

## Recap

- A proxy can be used to **quickly and anonymously** retrieve data from the Internet.
- A VPN can be used to **safely browse the Internet from public networks** or/and to stay hidden from **ISPs, hackers, governments..**.

![img_5](/networks/proxy/resources/proxy_vpn_nothing.jpg)




