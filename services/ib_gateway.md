# IB Gateway

> Interactive Brokers (IB) Gateway enables programmatic access to the IB platform for market data, order execution, and account management.

## Architecture & Infrastructure

* **Container Image:** Use the prebuilt Docker image from GitHub: [gnzsnz/ib-gateway-docker](https://github.com/gnzsnz/ib-gateway-docker).
* **Runtime:** The gateway runs on a **GCP Virtual Machine** inside a **VPC** with a **static IP**.
* **Networking:** The VM firewall allows inbound connections on the IB Gateway ports. This enables **Google Cloud Run jobs** to reach the gateway.
* **Diagram:**
  ![IB Gateway Infrastructure](/assets/ib_gateway.drawio.png)

## Authentication Constraint

* The **IBKR account used to authenticate the gateway must not be used elsewhere simultaneously**. If the same account logs into IBKR (e.g., via web or TWS), the gateway session is disconnected.

## Operating Modes

### Live Trading

* **Account model:** Use a **dedicated IBKR user** for the gateway. Multiple users can have access to the same portfolio, so the gateway account does not need to place trades directly.
* **Session policy:** IBKR allows a gateway session to run **up to 7 days** without restart.
* **Procedure:** Perform a **manual sign-in once per week**—**Sunday before trading resumes**—and keep the gateway running.

### Paper Trading

* **Account model:** The same IBKR user is used for both the gateway and manual trade entry.
* **Procedure:**

  * **Auto-start** the gateway a few minutes before the **production paper pipeline** runs.
  * **Shut down** the gateway afterward to allow the trader to enter orders.
* **MFA:** Paper gateway **does not require MFA**, which enables the automated start/stop approach.

## Summary

* Deploy the prebuilt Dockerized IB Gateway on a GCP VM within a VPC and static IP.
* Open only the required IB Gateway ports to permit Cloud Run jobs to connect.
* Do **not** reuse the authenticated account in parallel sessions.
* **Live:** dedicated gateway user, manual weekly login, 7-day session.
* **Paper:** shared user, automated short-lived sessions around the pipeline, no MFA.
