# homelab

## Layer 1 Network

- ISP: GloFiber 1.2 Gbps bidirectional
- Router: [Cloud Gateway Max](https://store.ui.com/us/en/category/cloud-gateways-compact/collections/cloud-gateway-max/products/ucg-max-ns?variant=ucg-max-ns)
- PoE Switchs:
  - [8 port Flex 2.5G PoE](https://store.ui.com/us/en/category/all-switching/products/usw-flex-2-5g-8-poe) - located in the living room closet
  - [8 port Lite PoE](https://store.ui.com/us/en/category/all-switching/products/usw-lite-8-poe) - located in the upstairs office
- APs:
  - [U7 Pro Max](https://store.ui.com/us/en/category/all-wifi/products/u7-pro-max) - 2nd floor Office AP
  - [U7 Pro](https://store.ui.com/us/en/category/wifi-flagship/products/u7-pro) - 1st floor Living Room AP

 ```mermaid
graph TD
  A["Internet<br>1.2 Gbit<br>Living Room"] -->|WAN| B["Router<br>Cloud Max 4-port 2.5 Gbit<br>Living Room"]
  B --> D["Switch<br>PoE 8-port 2.5 Gbit<br>Living Room"]
  B --> E["Switch<br>PoE 8-port 1 Gbit<br>Office"]
  B --> F["2x Empty"]
  D --> G["AP<br>U7 Pro Max<br>Upstairs"]
  D --> H["Laptop<br>Mom 1 Gbit<br>Living Room"]
  D --> C["Server<br>UnRAID 1 Gbit<br>Living Room"]
  D --> I["AP<br>U7 Pro<br>Living Room"]
  D --> J["4x Empty"]
%%  D --> K[Empty]
%%  D --> L[Empty]
%%  D --> M[Empty]
  E --> N["4x Empty"]
%%  E --> O[Empty]
  E --> P["Server<br>Morefine HA 1 Gbit<br>Office"]
  E --> Q["PC<br>Son 1 Gbit<br>Office"]
  E --> R["Arlo (gone soon)"]
%%  E --> S[Empty]
%%  E --> T[Empty]
```


## Hardware

## Containers
