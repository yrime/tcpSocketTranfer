import socket  # Import socket module
import argparse

class isServer:

    def run(self):

        s = socket.socket()  # Create a socket object
        host = 'localhost'  # Get local machine name
        port = 21225  # Reserve a port for your service.
        s.bind((host, port))  # Bind to the port
        print("Server bind", host, port)
        #f = open('torecv.png', 'wb')
        s.listen(5)  # Now wait for client connection.
        while True:
            c, addr = s.accept()  # Establish connection with client.
            print('Got connection from', addr)
            print("Receiving...")
            fileName = c.recv(1024).decode('utf-8')
            print("Create file", fileName)
            file = open(fileName, 'wb+')
            l = c.recv(1024)
            while (l):
                print("Receiving...", len(l))
                file.write(l)
                l = c.recv(1024)
            file.close()
            print("Done Receiving")
            #c.send('Thank you for connecting')
            c.close()
            exit()

class isClient:

    def run(self, fileName, file, host):

        s = socket.socket()  # Create a socket object
        #host = socket.gethostname()  # Get local machine name
        port = 21225  # Reserve a port for your service.

        s.connect((host, port))
        print("connection to",host,port)
        s.send(fileName.encode('utf-8'))
        f = open(file, 'rb')
        print('Sending file...',file)
        l = f.read(1024)
        while (l):
            print('Sending...',len(l))
            s.send(l)
            l = f.read(1024)
        f.close()
        print("Done Sending")
        s.shutdown(socket.SHUT_WR)
       # print(s.recv(1024))
        s.close()


# Press the green button in the gutter to run the script.
if __name__ == '__main__':
    parser = argparse.ArgumentParser()

    parser.add_argument("-o", "--fileoutput", type=str, help="Create file on the server")
    parser.add_argument('-s', "--server", action="store_true", help="Server mode")
    parser.add_argument('-f', "--file", type=str, help="File to sending")
    parser.add_argument('-a', "--host", type=str, help="Host address")

    args = parser.parse_args()

    if args.server:
        print("Server run...")
        serv = isServer()
        serv.run()
    else:
        cli = isClient()
        cli.run(args.fileoutput, args.file, args.host)
