# Weighted-Fair-Queuing-WFQ

Weighted Fair Queuing (WFQ) is a packet scheduling algorithm used in routers and network switches to decide which packet should be transmitted next.

Instead of sending packets in the order they arrive, WFQ ensures that:
- Every flow (or user) gets a fair share of the link
- Some flows can be given higher priority using "weights"
- Large packets do not unfairly block small packets
- Traffic is scheduled in a way that resembles bit by bit sharing 

WFQ is designed to approximate an idealized fluid-flow model called General Processor Sharing (GPS) where every flow gets service in proportion to its weight.

A regular FIFO (First in First Out) queue is unfair because:
- A flow with large packets can delay others
- A single heavy flow can dominate bandwidth
- Important flows (like voice or video) cannot be prioritized
- All packets are treated equally even if some should be more “important”

WFQ solves these problems by giving each flow its own virtual queue and scheduling packets based on virtual finish times.

WFQ calculates a finish time for each packet as if the link were serving all flows bit-by-bit in parallel.

The finish time is computed using:
- The packet’s arrival time
- The previous finish time of that flow
- The packet length
- The flow’s weight

Then, the router always sends the packet with the earliest finish time. This ensures a flow with weight 2 gets twice as much bandwidth as a weight-1 flow.