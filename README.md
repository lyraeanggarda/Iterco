# Unreal Engine Tasks

This project demonstates Unreal Engine's Server-Authoritative. It covers Authority & Replication, Remote Procedure Calls (RPCs), and Ownership & Relevancy

**[Short Video](https://drive.google.com/file/d/10GQdd3Y5RwlMeVREXQxzj7dLgIIOJV6t/view?usp=sharing)**
 
## Task 1 - Authority & Replication
Implement an Health System with server authority. Created an Actor with a Health variable set to RepNotify to call a function automatically when value is changed.

Health is modified only on the server. Clients must call a Server RPC to request changes.

If Server tries to modify Health, the health will automatically changed for all the clients.

If Client tries to modify Health, the health only changes for itself

Visual for color and name text is based on the Authority. Green for Server and Red for Client

## Task 2 - RPC Implementation
Impement a Fire action for a Character using Server RPC and Multicast

Input is handled on Client (BP_CharacterProjectile) and Client calls ServerFire (Run on Serever)

Validate using variable Ammo (Integer) and bCanFire (Boolean)

For Server Logic, Spawn Projectile, decrement ammo and timer for bCanFire

For Multicast, Spawn System at Location (Muzzle Break) to replicate to all clients

## Task 3 - Ownership & Relevancy
Implement data that can see by all clients, only to owning client, and certain range

For visible to all clients, using bIsLooted (boolean) variable set to RepNotify to call a function change it shape to sphere when bIsLooted is true. So all clients can see if the shape is changed

For owning client, Spawn a widget "You've got an Item" when colliding to Sphere collision using Client RPC on PlayerController

RPCs must be called from owned actors

For Relevancy set **Net Cull Distance Squared** to 500,000. So the actor only replicates to nearby players. When it far away from the actor, bIsLooted will stay at false until the Character close enough to the actor

## Optional - Seamless Level Travel
Implement seamless level travel to move players from One level to another level.

Need Advanced Sessions plugin to use Travel Function

In GameMode, bUseSeamlessTravel needs to set to true and Travel Call using the Level Name
