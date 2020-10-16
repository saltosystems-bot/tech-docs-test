---
title: "Glossary"
---

| Name             | Description |
|------------------|-------------|
| **Access point** | Represents a smart electronic device capable of granting or denying access to a secured area, such as a room, office, apartment, etc. It may also serve to lock/unlock secured containers like cabinets, drawers or lockers. In the real world, it can take on different forms, for example: a door equipped with an electronic escutcheon or cylinder, a control unit (with an electric strike), a padlock, etc. In general, a credential (see [Key](#key)) must be presented for the access point to grant access. |
| **Access right** | Represents a materialized view of access permissions. It is intended to simplify the management of access permissions for large sets of users with similar access profiles. An access right can be associated with multiple access points. |
| **Device** | A device is a piece of hardware that can be used in the Nebula system. Although an access point is also a device, for the purposes of the API a device refers to a more peripheral piece of hardware such as a gateway, encoder or repeater. |
| **Event** | Describes activity which takes place within an installation and can relate to individual access points. For example, depending on a user's permissions they can see when an access point was created, whether an access point has been deleted or updated, or when an access point was opened and by which user etc. |
| **Gateway** | Gateways are hardware devices intended to be used with access points where online connectivity is needed. |
| **Installation** | Represents a collection of all the access control objects (such as access points, access rights, users, etc.) that comprise the access control system within a customer’s facility. |
| **<a name="key"></a>Key** | There are two types of keys in the Nebula API. A **card key** refers to a physical key such as a fob, wristband or keycard. Card keys can be encoded using an online access point. An **app key** is a type of mobile key that you can use via the SALTO Nebula app. |
| **Repeater** | A repeater allows the distance between a gateway and an access point to be extended. It forwards signals between an access point and a gateway. |
| **User** | Can refer to both an owner of keys and a user with permissions to manage other users within Nebula. Users are eligible to access rights and may be assigned a key. |
