// connect to the IP address 130.208.242.120. Find a port between 4000 and 4100 that is open.

#include <iostream>
#include <string>
#include <sstream>
#include <fstream>
#include <vector>
#include <cstdlib>
#include <ctime>
#include <unistd.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netdb.h>
#include <arpa/inet.h>

using namespace std;

int portSniffer(string ip, int portMin, int portMax){
    // Lookup the hostname
    struct hostent *host = gethostbyname(ip.c_str());
    // Create the socket
    int sock = socket(AF_INET, SOCK_STREAM, 0);
    // Set timeout for socket oerations
    struct timeval tv;
    tv.tv_sec = 1;
    tv.tv_usec = 0;
    setsockopt(sock, SOL_SOCKET, SO_RCVTIMEO, (char *)&tv, sizeof(struct timeval));
    
    // Create the sockaddr_in structure
    struct sockaddr_in sin;
    sin.sin_family = AF_INET;
    sin.sin_addr = *((struct in_addr *)host->h_addr);
    for(int i = portMin; i <= portMax; i++){
        sin.sin_port = htons(i);
        // Connect to the server
        if(connect(sock, (struct sockaddr *)&sin, sizeof(sin)) < 0){
            cout << "Port " << i << " is closed" << endl;
        } else {
            cout << "Port " << i << " is open" << endl;
            close(sock);
            sock = socket(AF_INET, SOCK_STREAM, 0);
            tv.tv_sec = 1;
            tv.tv_usec = 0;
            setsockopt(sock, SOL_SOCKET, SO_RCVTIMEO, (char *)&tv, sizeof(struct timeval));
        }
    }
    close(sock);
    
    return 0;
    // Scan the ports
}


int main(int argc, char *argv[])
{
    // string ip = argv[1];
    // int portMin = atoi(argv[2]);
    // int portMax = atoi(argv[3]);
    //int openPort = portSniffer(ip, portMin, portMax);
    int openPort = portSniffer("130.208.242.120", 4000, 4100);
    cout << "Open Port: " << openPort << endl;
    return 0;
}
