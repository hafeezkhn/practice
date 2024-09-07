--> Pre 
     a. Automotive Ethernet (TCP/IP satck)
     b. Socket Programming
     c. Packet structures and protocols(IP,TCP,UDP,Ethernet)

--> OSI stack :A,P,S,T,N,D,P
              : connect any two computers to exchnge data

--> TCP/IP : use services over internet
           :Server offer services,client uses services,
           :A,T,N,Host to network layer(D+P)
           
           - APP layer:FTP,SOMEIP,AVB,Diagnostic over IP(DoIP)
           - Transport:TCP/UDP 
           - Network  :IP
           - D+P      : Ethernet,Automotive ethernet

--> singnal orented Archi vs service oriented Archi(SOA) 


--> SOME/IP: the Enabler of SOA in Automotive networks
           - (Scalable service-oriented Middleware over IP)designed to make ethernet data transfer compatible with communication demands of Automotive ECUs.
           - SomeIP handles data-serialization,RPC(remote procedure call) and other essential tasks.
           -service req one ECU and Service provider another ecu works through sockets programming.

          --------        auto       -------
         | ECU 1  |-----------------| ECU 2 |
          --------    eth(TCP/IP)    -------
         publisher                  subscriber
            |                           |
    provides service            establish connection
            |                           |
  form of running program           process 2
        (process 1)                 (Reciver)
            |                           |
    process runs on a           runs on specific port no.
    specific port no.                   |   
(read/write data to process             |
       using ports)                     |
            |                           |
  combination of IP addr             (Socket)
  and port no.(socket) 
 

--> In SOA

 Publisher-offers(multiple) <-> Subscriber(wants to use any service)              
     \   \  \                                   / 
      \   \  service 1                 service 2(service discover)
       \   \    
        \   service 2
         \  
          service 3


 --> SOME/IP
     a. Basic Principle
     b. Service Discovery
     c. Service offerings
     d. Header format

--> Why SOME/IP?
    model the entire system as service interface(interportab/high bandwidth)
    send data to only receiver that needs it (all nodes dont have to hear)
    
--> Need for middleware(irrespective of  application):
      - to handle remote procedure calls,serialization
      - need to support Publish-subscribe model
      - Service Discovery
      - Segmentation of messages

NOTE: we can say middleware based on SOA is SOMEIP,scalable coz 
different platforms,service oriented coz Client-server,
over IP coz ethernet based.

           client |               | server
            app   |               | app
           -------------------------------
          |       SOMEIP Middleware       |
           -------------------------------
           TCP/IP |               |TCP/IP
            stack |<------------->| stack



