Have you built a utility for Learning Registry? List it here.
Have you extended core Learning Registry? List it here.

# External Utilities

## Data Pumps

### LRDataPump
Harvests an OAI-PMH NSDL_DC repository and publishes as signed LR resource data to a specific node. Utility is designed to work as a differential task. Subsequent execution will harvest from the configured repository since the last successful harvest. Tool is also resumable, if for some reason a failure occurs, the next run will pick up harvesting where it left off, and not republish.

> Language: Python

> License: Apache 2

> Author: Jim Klo (SRI International)

> URL: [https://github.com/jimklo/LRDataPump](https://github.com/jimklo/LRDataPump)


## Envelope Signing

### LRSignature
Extendable Python library and command line tools that can be used to sign LR resource data documents.

> Language: Python

> License: Apache 2

> Author: Jim Klo (SRI International)

> URL: [https://github.com/jimklo/LRSignature](https://github.com/jimklo/LRSignature)