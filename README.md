tor-node-map
======

See it here: [http://cdetrio.github.io/tor-node-map/](http://cdetrio.github.io/tor-node-map/)


Uses tor relay information from [https://onionoo.torproject.org/](https://onionoo.torproject.org/). Plots relay nodes as bubbles (circles) with area proportional to their observed bandwidth. The bubbles are plotted on a [kinetic.js](http://kineticjs.com/) canvas, overlayed on top of a [d3.js](http://d3js.org/) map. I did it this way (kinetic/d3 mashup) for better performance. On my machine, panning/zooming more than a few hundred d3 svg elements is too slow. But it can comfortably handle a few thousand canvas sprites. Kineticjs provides event handlers on canvas sprites, d3 does not. Firefox needs an offsetX/Y event property kludge, so relay selection works a little bit better in Chrome.

One issue to be fixed is when multiple relays have the same geoip latitude/longitude coordinates. Where this happens, you will see lots of white as several bubbles of different sizes are placed at the exact same spot (each bubble has a thin white outline stroke). I'm not yet sure how to deal with this.

There's also a group of bubbles in the top-left (0,0), these are relays with ip addresses not in the geoip database.

To fetch latest relay details from onionoo: `wget https://onionoo.torproject.org/details?type=relay -O onionoo-relay-details.json`

To run a local webserver: `python -m SimpleHTTPServer`


inspired by 
[jordan-wright/tormap](https://github.com/jordan-wright/tormap)
[http://raidersec.blogspot.com/2013/09/mapping-tor-relays-and-exit-nodes.html](http://raidersec.blogspot.com/2013/09/mapping-tor-relays-and-exit-nodes.html)


Incentive for Tor Relays - proof-of-relay / proof-of-bandwidth
------
Currently, Tor relay bandwidths are [estimated by active measurements](https://blog.torproject.org/blog/lifecycle-of-a-new-relay), performed by a set of "bandwidth authorities" (bwauths). The bandwidth authorities vote to form a "consensus bandwidth" (listed as "consensus_weight" in onionoo) value for a relay.

[LIRA](http://freehaven.net/anonbib/cache/ndss13-lira.pdf) is an incentive scheme for Tor relays - think of it as "TorCoin". LIRA proposes using an opportunistic [decentralized bandwidth measurement](https://trac.torproject.org/projects/tor/ticket/5464), namely [EigenSpeed](https://www.usenix.org/legacy/event/iptps09/tech/full_papers/snader/snader.pdf), instead of active measurements by bandwidth authorities. In a decentralized EigenSpeed measurement, each node would communicate to others its estimate of other nodes' bandwidths. The result would be each node maintaining its own large sparse [EigenTrust](https://en.wikipedia.org/wiki/EigenTrust)-like matrix.


Other tor relay maps:
------
[Vidalia Network Map](https://tails.boum.org/doc/anonymous_internet/vidalia/index.en.html#index1h1)

[Vidalia Network Map using Marble 3D Globe](https://blog.torproject.org/blog/technology-preview-marble-and-vidalia020)

[Tore Metrics - Network Bubbles](https://metrics.torproject.org/bubbles.html)

[void.gr world map](https://tormap.void.gr/) - [World City Map of Tor Nodes](http://www.void.gr/kargig/blog/2012/11/27/world-city-map-of-tor-nodes/)

[Visualization: Tor nodes on Google Maps and Google Earth](http://moblog.wiredwings.com/archives/20101213/visualization-tor-nodes-on-google-maps-and-google-earth.html)

[Tor exit nodes located and mapped](http://hackertarget.com/tor-exit-node-visualization/)

[Tor V3 consensus servers worldwide](http://freehaven.net/~ioerror/) (long load time)

[endast/Tormap](https://github.com/endast/Tormap/) - [http://bitly.com/tor_map](http://bitly.com/tor_map)


Other p2p network node maps:
------
[bitcoin nodes WebGL globe](http://blockchain.info/nodes-globe)
