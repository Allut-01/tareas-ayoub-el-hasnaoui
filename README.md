"mermaid"

    sequenceDiagram
    participant Client as User
    participant Server1 as DHCP Server #1
    participant Server2 as DHCP Server #2

    note "User  turns on computer and connects to network"
    Client->>Server1: Request IP address
    Server1->>Client: Assign IP address (lease time: 8 hours)

    note "User  works for 1 hour"
    Client->>Server1: Renew IP address
    Server1->>Client: Renew IP address (lease time: 8 hours)

    note "3-minute outage"
    Client->>Client: Reconnect to network
    note "Server #1 is down"
    Client->>Server2: Request IP address
    Server2->>Client: Assign IP address (lease time: 8 hours)

    note "User  remains active for 12 hours"
    Client->>Server2: Renew IP address
    Server2->>Client: Renew IP address (lease time: 8 hours)

    note "User  disconnects for 1 hour"
    Client->>Client: Disconnect from network

    note "User  reconnects to network"
    Client->>Server2: Request IP address
    Server2->>Client: Assign IP address (lease time: 8 hours)

    note "User  stays on network for 5 hours"
    Client->>Server2: Renew IP address
    Server2->>Client: Renew IP address (lease time: 8 hours)

    note "User  disconnects permanently"
    Client->>Client: Disconnect from network

  "mermaid"
