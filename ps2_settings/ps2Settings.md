# PS2 Settings and PC Optimizations

A collection of my settings and optimizations. Mileage may vary.

<span style="color:red;font-size:18px">
I am in no way responsible if you somehow manage to break something.
</span>

## My Specs

Here are my specs so you have a reference point to compare to.

CPU: AMD 5800x @ 4.6Ghz (Overclocked)
RAM: Crucial 64GB @ 3600Mhz
GPU: Nvidia GTX 2080 Ti
SSD: Samsung 970 Evo Plus 1Tb M.2 SSD - Game drive only. OS is on a separate M.2.

---

## Windows Optimizations

### Nagle's Algorithm

I disable this to reduce latency to the server. Basically it waits to fill up a network packet with data - in our case, PS2 game updates - before sending it all at once. By disabling the algo, our computer will send more frequent updates and reduce our latency to the server at the cost of wasted space in the packet and higher bandwidth consumption. You shouldn't have to worry about this with modern networks unless you're on a data cap or a poor connection.

<span style="color:red;font-size:18px">
**WARNING**
</span>

This involves editing the registry. Do not mess with anything else in here unless you want to introduce problems.

**Grab your primary network adapter's IPv4 address**
1. `Right-click` on the `Start Menu` icon.
2. Select `Run`.
3. Type `cmd` into the bar and press `OK`.
4. In the black window that shows up, type in `ipconfig /all` and press `Enter`.
5. Save the `IPv4 address` of your primary network adapter. We will use this later. 
   - Typically, the correct adapter will have your ISP name show up under `Connection-specific DNS Suffix`.

![ipconfig example](/ps2_settings/images/ipconfig.png)

**Disabling Nagle's Algorithm**
1. `Right-click` on the `Start Menu` icon.
2. Select `Run`.
3. Type in `regedit` and press `Ok`.
4. Copy and paste this registry path into the bar at the top and press `Enter`.
  `Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces`
5. You will see several folders here with a format similar to  `{5f20981e-2b8e-48b7-9c09-47814b179c16}` corresponding to each of the network adapters on your computer. Go through each one and locate the folder where the `DhcpIPAddress` matches the `IPv4 address` we found earlier. You should also see the `DhcpDomain` match the `Connection-specific DNS Suffix` as well.
6. Once you have the right folder, `Right-click` on it and select `New` > `DWORD (32-bit) Value`. Using this method, create two new entries with the following information:
   - DWORD 1
     - Value name: `TcpAckFrequency`
     - Value data: `1`
     - Base: `Hexadecimal`
   - DWORD 2
     - Value name: `TCPNoDelay`
     - Value data: `1`
     - Base: `Hexadecimal`
7. You should end up with two keys that look like this if done correctly:
   ![nagles](images/nagles.png)
8. Restart your computer.

--- 

### CPU Core Parking

CPU core parking is a CPU power optimization that downclocks your CPU cores when not under load to decrease heat and power consumption. It takes time for your cores to ramp back up to full speed and results in lower and stuttery FPS performance. Disabling core parking will result in smoother and higher FPS performance at the cost of more heat and a higher base power consumption.

There are a few programs out there that can disable CPU core parking. My favorite is [QuickCPU](https://coderbag.com/product/quickcpu). 