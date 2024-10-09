 # DHCP Service Request Schema

## Assignment

Crear un esquema de solicitud de servicio DHCP para un usuario que se conecta a una red con dos servidores DHCP. El usuario permanece conectado durante 1 hora, experimenta un apagón de 3 minutos, se reconecta y permanece activo durante 12 horas, se desconecta durante 1 hora y luego se reconecta y permanece en la red durante 5 horas antes de desconectarse permanentemente.

```mermaid
sequenceDiagram
    participant Client as Usuario
    participant Server1 as Servidor DHCP #1
    participant Server2 as Servidor DHCP #2

    note "Usuario enciende la computadora y se conecta a la red"
    Client->>Server1: Solicitud de dirección IP
    Server1->>Client: Asignación de dirección IP (tiempo de arrendamiento: 8 horas)

    note "Usuario trabaja durante 1 hora"
    Client->>Server1: Renovación de dirección IP
    Server1->>Client: Renovación de dirección IP (tiempo de arrendamiento: 8 horas)

    note "Apagón de 3 minutos"
    Client->>Client: Reconexión a la red
    note "Servidor #1 está caído"
    Client->>Server2: Solicitud de dirección IP
    Server2->>Client: Asignación de dirección IP (tiempo de arrendamiento: 8 horas)

    note "Usuario permanece activo durante 12 horas"
    Client->>Server2: Renovación de dirección IP
    Server2->>Client: Renovación de dirección IP (tiempo de arrendamiento: 8 horas)

    note "Usuario se desconecta durante 1 hora"
    Client->>Client: Desconexión de la red

    note "Usuario se reconecta a la red"
    Client->>Server2: Solicitud de dirección IP
    Server2->>Client: Asignación de dirección IP (tiempo de arrendamiento: 8 horas)

    note "Usuario permanece en la red durante 5 horas"
    Client->>Server2: Renovación de dirección IP
    Server2->>Client: Renovación de dirección IP (tiempo de arrendamiento: 8 horas)

    note "Usuario se desconecta permanentemente"
    Client->>Client: Desconexión de la red
```
