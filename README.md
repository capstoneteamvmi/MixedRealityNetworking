# MixedRealityNetworking (Built for Unity and UWP)

This library was built because of the incompatibility between Unity with .NET 2.0, UWP with .NET core and .NET 4.6 socket libraries.

You can use this library to set up basic communication between an Unity client and an UWP client. We're using this library between Unity and a Hololens for network communication. It gives you the freedom to change and implement your own protocols.

## How to use

1. Compile the both projects to a .DLL file
2. Import both .DLLs into your Unity project into the Plugins folder
3. Select the UnityNetworking.dll, and in the inspector "Select platform for plugin", only check the Editor (make sure you are including platforms, not excluding).
4. Select the UWPNetworking.dll, and in the inspector, only check WSAPlayer

When you've done this, you can start using the MixedRealityNetworking namespace in your Unity project. The .DLL should work both on desktop PC's and on UWP devices such as the Hololens. Make sure that if you implement your own methods into the library that the methods are the same in BOTH DLL's.

## Why was this library build?

We've tried using all kinds of networking solutions for our project with Unity and a Hololens. Unity's standard networkinglibrary "UNet" had a lot of overhead, and was not easy to integrate into our project. Microsoft released a Holotoolkit for the Hololens in combination with Unity. However, this library is not fully opensource and only runs on Windows. Because the protocol is not opensource, you can't implement it into a dedicated Linux server. Using plain C# sockets didn't work because the System.Net.Sockets namespace is not available in UWP, and libraries designed for UWP to make the namespace available, couldn't be installed because Unity runs on .NET 2.0. So we've build our own.

This library gives you just a small layer on top of the UDP protocol, meaning you can send every data you want. It's very easy in use and easily expendable for use in your own project. You can use it peer2peer, but you can also implement a dedicated server for example.

## Extra information

UDP does not automatically know clients, like a TCP socket. Before a client is known, it should send a message first. If you are having problems with connecting 2 clients, please make sure your firewall allows the UDP traffic and the IP addresses and ports are correct. You could work around p2p issues by using a dedicated server which routes the UDP traffic to the right client. But even then; all clients should send a message first to the server before the client is known. The server should store the IP address and the port.