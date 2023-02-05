### FAU Team 1 MITRE eCTF Design Reference

# Security Requirements

_**SR1: A car should only unlock and start when the user has an authentic fob that is paired with the car**_

In our design, a car will require a valid secret from a paired fob. If the secret is incorrect, the car will not unlock and will not start.

_**SR2: Revoking an attacker’s physical access to a fob should also revoke their ability to unlock the associated car**_

A paired fob must store a pairing pin an and unlock key for the corresponding car. These values will be stored securely in EEPROM such that it will be difficult for an attacker with physical access to recover the key. Additionally, efforts will be made to secure the fob from fault injection attacks that might leak, or give access to, secret data.

_**SR3: Observing the communications between a fob and a car while unlocking should not allow an attacker to unlock the car in the future**_

We will secure communication between the paired fob and the car using TLS and AES such that it will be very difficult for the attacker to read communications. The pairing pin will be used to modify the secret unlock key such that if an attacker does successfully record communication, they will need the pairing pin to perform an unlock.

_**SR4: Having an unpaired fob should not allow an attacker to unlock a car without a corresponding paired fob and pairing PIN**_

In our design, the pairing process will always produce a result that is stored in the unpaired fob. If the pairing pin or password is incorrect, the secret unlock key given to the unpaired fob will be incorrect, preventing access to the car. Secrets in the paired fob will be stored securely in EEPROM preventing access from the attacker.

_**SR5: A car owner should not be able to add new features to a fob that did not get packaged by the manufacturer**_

In our design, each car will be assigned a random unique id. This id will be used to digitally sign feature packages that the target fob must verify came from the manufacturer.

_**SR6: Access to a feature packaged for one car should not allow an attacker to enable the same feature on another car**_

Each packaged feature will be signed with a unique car id. If one car's feature was provided to another car's fob, the signature would fail verification, preventing the enabling of that feature.


