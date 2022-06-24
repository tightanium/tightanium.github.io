# PS2 Settings and PC Optimizations

A collection of settings and optimizations I run on every Windows install for a better gaming experience. Mileage may vary.

```diff
- I am in no way responsible if you somehow manage to break something
```

## Windows Optimizations

### Nagle's Algorithm

Nagle's algorithm is a network optimization that can be detrimental to in-game latency. For the sake of keeping things simple, think of a network packet as a large box with a fixed size and the network is UPS. Nagle's algorithm tries to fill up that box with all the tiny updates about the game before sending it off through the network. This is great for improving the overall efficiency of the network but, not so great when you want things to register with the server as fast as possible. By disabling the algorithm, our machine will send out updates to the server more frequently at the cost of shipping one or two tiny updates in a huge box and wasting bandwidth. Thankfully, the wasted bandwidth isn't a huge issue with modern networks but, can you imagine shipping these wasted boxes on dial-up?

