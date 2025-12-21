flowchart TB
    %% =========================
    %% MANAGEMENT LAYER
    %% =========================
    subgraph MGMT["Management Zone"]
        VC[vCenter 8.0.3]
        NSX[NSX Manager 4.2.x]
    end

    %% =========================
    %% ESXi CLUSTER
    %% =========================
    subgraph CLUSTER["4-Node ESXi 8.0.3 Cluster (VDS + NSX Overlay)"]
        
        %% USER ZONE
        subgraph USER["User Zone (SEG-USER)"]
            JUMP[Jumpbox / Admin VM]
            ATTACK[Attack VM (Lab Only)]
        end

        %% APP ZONE
        subgraph APP["Application Zone (SEG-APP)"]
            WEB[Web Server]
            APPVM[Application Server]
        end

        %% DB ZONE
        subgraph DB["Database Zone (SEG-DB)"]
            DBVM[(MySQL / MS SQL)]
        end

        %% IOT ZONE
        subgraph IOT["IoT Zone (SEG-IOT)"]
            IOTSIM[IoT Simulator]
            IOTGW[IoT Gateway]
        end
    end

    %% =========================
    %% ALLOWED FLOWS (ZERO TRUST)
    %% =========================
    JUMP -->|SSH / RDP| WEB
    JUMP -->|SSH / RDP| APPVM
    JUMP -->|SSH / RDP| DBVM
    JUMP -->|SSH / RDP| IOTGW

    WEB -->|3306 / 1433| DBVM
    APPVM -->|3306 / 1433| DBVM

    IOTSIM -->|MQTT| IOTGW
    IOTGW -->|HTTPS| WEB

    %% =========================
    %% BLOCKED FLOWS (DFW)
    %% =========================
    IOTSIM -. BLOCKED .-> DBVM
    IOTSIM -. BLOCKED .-> APPVM
    WEB -. BLOCKED .-> IOTSIM
    DBVM -. BLOCKED .-> USER

    %% =========================
    %% MANAGEMENT CONNECTIONS
    %% =========================
    VC --- NSX
    VC --- CLUSTER
    NSX --- CLUSTER
