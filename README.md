# iperf3
This is a simple way for test your bandwith and throughput network on amazon-linux.

## Install iperf3
sudo yum --enablerepo=epel install iperf iperf3

1 - Server:
You must enter in your amazon-linux instance and start iperf3 as a server.
iperf3 -s -p 8080
flags:
	-s: server mode
	-p: port to listen

2 - Client:
iperf3 -c `server_ip` -i 1 -t 10 -V -p 80 -Z  -f M
flags:
	-c: client mode you have to put the server ip_address
    -i: interval that you use to send data between client and server
	-t: time
	-p: port where server is listening
	-Z: mode zero-copy
	-f: Format the output in megabytes

# Example:
The client and server are r3.xlarge and they have enabled ENA interfaces.

For know more about ENA on Amazon-Linux:

http://docs.aws.amazon.com/es_es/AWSEC2/latest/UserGuide/enhanced-networking.html#supported_instances

```
[root@ip-xxx-xxx-xxx-xxx ec2-user]# iperf3 -s -p 80
-----------------------------------------------------------
Server listening on 80
-----------------------------------------------------------
Accepted connection from xxx.xxx.xxx.xxx, port 48966
[  5] local xxx.xxx.xxxx.xxx port 80 connected to xxx.xxx.xxx.xxx port 48968
[ ID] Interval           Transfer     Bandwidth
[  5]   0.00-1.00   sec   408 MBytes  3.42 Gbits/sec
[  5]   1.00-2.00   sec  81.2 MBytes   681 Mbits/sec
[  5]   2.00-3.00   sec  81.0 MBytes   680 Mbits/sec
[  5]   3.00-4.00   sec  81.5 MBytes   684 Mbits/sec
[  5]   4.00-5.00   sec  82.6 MBytes   693 Mbits/sec
[  5]   5.00-6.00   sec  82.6 MBytes   693 Mbits/sec
[  5]   6.00-7.00   sec  82.6 MBytes   693 Mbits/sec
[  5]   7.00-8.00   sec  82.6 MBytes   693 Mbits/sec
[  5]   8.00-9.00   sec  82.6 MBytes   693 Mbits/sec
[  5]   9.00-10.00  sec  82.6 MBytes   693 Mbits/sec
[  5]  10.00-10.05  sec  3.88 MBytes   690 Mbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[  5]   0.00-10.05  sec  0.00 Bytes  0.00 bits/sec                  sender
[  5]   0.00-10.05  sec  1.12 GBytes   961 Mbits/sec                  receiver
```
```
[root@ip-xxx.xxx.xxx.xxx ec2-user]# iperf3 -c xxx.xxx.xxx.xxx -i 1 -t 10 -V -p 80 -Z  -f M
iperf 3.0.12
Linux ip-xxx.xxx.xxx.xxx 4.4.19-29.55.amzn1.x86_64 #1 SMP Mon Aug 29 23:29:40 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux
Time: Sat, 28 Jan 2017 10:57:32 GMT
Connecting to host xxx.xxx.xxx.xxx, port 80
      Cookie: ip-xxx.xxx.xxx.xxx.1485601052.711979
      TCP MSS: 8949 (default)
[  4] local xxx.xxx.xxx.xxx port 48968 connected to xxx.xxx.xxx.xxx port 80
Starting Test: protocol: TCP, 1 streams, 131072 byte blocks, omitting 0 seconds, 10 second test
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  4]   0.00-1.00   sec   414 MBytes   414 MBytes/sec  169    760 KBytes
[  4]   1.00-2.00   sec  81.2 MBytes  81.3 MBytes/sec    1    891 KBytes
[  4]   2.00-3.00   sec  80.0 MBytes  80.0 MBytes/sec    8    717 KBytes
[  4]   3.00-4.00   sec  82.5 MBytes  82.5 MBytes/sec    0   1.11 MBytes
[  4]   4.00-5.00   sec  82.5 MBytes  82.5 MBytes/sec    4   1.12 MBytes
[  4]   5.00-6.00   sec  82.5 MBytes  82.5 MBytes/sec    4   1.07 MBytes
[  4]   6.00-7.00   sec  82.5 MBytes  82.5 MBytes/sec    3   1.02 MBytes
[  4]   7.00-8.00   sec  82.5 MBytes  82.5 MBytes/sec    4   1014 KBytes
[  4]   8.00-9.00   sec  82.5 MBytes  82.5 MBytes/sec   13    682 KBytes
[  4]   9.00-10.00  sec  82.5 MBytes  82.5 MBytes/sec    1    996 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
Test Complete. Summary Results:
[ ID] Interval           Transfer     Bandwidth       Retr
[  4]   0.00-10.00  sec  1.13 GBytes   115 MBytes/sec  207             sender
[  4]   0.00-10.00  sec  1.12 GBytes   115 MBytes/sec                  receiver
CPU Utilization: local/sender 1.1% (0.1%u/1.2%s), remote/receiver 6.9% (0.5%u/6.5%s)
```

## Results:

You have tranfered 1.13 GBytes in 10 seconds with a Bandwidth 115 MBytes/sec, you can see and review such second in the output, too yo can see how Retr(retransmisisons) or CWND(congestion window) you have.

## More info:
https://fasterdata.es.net/performance-testing
 
