 # DHCP Service Request Schema

## Assignment

Crear un esquema de solicitud de servicio DHCP para un usuario que se conecta a una red con dos servidores DHCP. El usuario permanece conectado durante 1 hora, experimenta un apagón de 3 minutos, se reconecta y permanece activo durante 12 horas, se desconecta durante 1 hora y luego se reconecta y permanece en la red durante 5 horas antes de desconectarse permanentemente.

```mermaid
sequenceDiagram
    participant Client as User
    participant Server1 as DHCP Server1
    participant Server2 as DHCP Server2

    %% User turns on computer and connects to network
    Client->>Server1: Request IP address
    Server1->>Client: Assign IP address (lease time: 8 hours)

    %% User works for 1 hour
    Client->>Server1: Renew IP address
    Server1->>Client: Renew IP address (lease time: 8 hours)

    %% 3-minute outage
    Client->>Client: Reconnect to network
    Client->>Server2: Request IP address
    Server2->>Client: Assign IP address (lease time: 8 hours)

    %% User remains active for 12 hours
    Client->>Server2: Renew IP address
    Server2->>Client: Renew IP address (lease time: 8 hours)

    %% User disconnects for 1 hour
    Client->>Client: Disconnect from network

    %% User reconnects to network
    Client->>Server2: Request IP address
    Server2->>Client: Assign IP address (lease time: 8 hours)

    %% User stays on network for 5 hours
    Client->>Server2: Renew IP address
    Server2->>Client: Renew IP address (lease time: 8 hours)

    %% User disconnects permanently
    Client->>Client: Disconnect from network
