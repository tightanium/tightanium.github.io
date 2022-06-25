# PS2 Settings and PC Optimizations

A collection of settings and optimizations I run on every Windows install for a better gaming experience. Mileage may vary.

```diff
- I am in no way responsible if you somehow manage to break something. However, I am willing to try to help you with your problem.
```

---

## Windows Optimizations

### Nagle's Algorithm

I disable this to reduce latency to the server. Basically it waits to fill up a packet with data - in our case, PS2 game updates - before sending it all at once. By disabling the algo, our computer will send more frequent updates and reduce our latency to the server at the cost of wasted space in the packet and higher bandwidth consumption. You shouldn't have to worry about this with modern networks unless you're on a data cap or a poor connection.

#### How To Disable Nagle's Algorithm

**WARNING**
```diff
- This involves editing the registry. Do not mess with anything else in here unless you want to introduce problems.
```

**Grab your primary network adapter's IPv4 address**
1. `Right-click` on the `Start Menu` icon.
2. Select `Run`.
3. Type `cmd` into the bar and press `OK`.
4. In the black window that shows up, type in `ipconfig /all` and press `Enter`.
5. Save the `IPv4 address` of your primary network adapter. We will use this later. 
   - Typically, the correct adapter will have your ISP name show up under `Connection-specific DNS Suffix`.

![ipconfig example](/images/ipconfig.png)

**Disabling Nagle's Algorithm**
1. `Right-click` on the `Start Menu` icon.
2. Select `Run`.
3. Type in `regedit` and press `Ok`.
4. Copy and paste this registry path into the bar at the top and press `Enter`.
   `Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces`
5. You will see several keys here with a format similar to  `{5f20981e-2b8e-48b7-9c09-47814b179c16}` corresponding to each of the network adapters on your computer. Go through each one and locate the key with the `DhcpIPAddress` matching the `IPv4 address` we found earlier. You should also see the `DhcpDomain` match the `Connection-specific DNS Suffix` as well.
6. 