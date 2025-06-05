The setup I have is an XPenology system with an Intel Core i3 14100 with 16GB of RAM with 6 HDDs totalling 61TB Raw

Might not be fancy, but it does the work.

The Networking of the system consists of 2 containers runningg Nginx Proxy Manager, one under a Macvlan for public facing containers and one internal only. The access for the internal containers that have sensitive informatiton happens via WireGuard tunnel with the connection entering via an Omada VPN Router.  