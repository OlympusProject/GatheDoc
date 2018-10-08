# Warehouse User Management

This service should be developed under ```com.zeus.service.management```

This service will manage any warehouse user and their storages.

## Definition

___Warehouse___ is the physical building where things are stored.

___WarehouseUser___ is any individual/group/company who stores their items in the given ___Warehouse___.

___WarehouseUser___ can be the __owner__ of the warehouses, or __another__ individual/group/company that'd like to rent for storages.

The owner of the ___Warehouse___ can be more than one individual/group/company.

___InboundOrder___ is the order statement to put the items of ___WarehouseUser___ to the given ___Warehouse___.

Don't mix the ___Item___ and item in this context. ___Item___ is the term for what kind of item registered in the system. item is just item in general.

## The System

The ___WarehouseUser___ must be registered first before making any ___InboundOrder___ alongside the maximum capacity of storage they'd like to use.

___WarehouseUser___ will own the ___Warehouse___ space for limited time with ___Subscription___ system.

___WarehouseUser___ with different ___Tier___ will have different limit of space that they can use.

### WarehouseUser Tier

_Basic_ user can only acquire limited space in one ___Warehouse___.

_Standard_ user can only acquire limited space in any ___Warehouse___ the owner has. This tier upwards support inter-warehouse transfer.

_Premium_ user can have unlimited space in all warehouses, with the exception if the designated warehouse already full for some reason.

_Unicorn_ user is the user that really want a warehouse for itself, but don't want to bother of managing the items. Basically, we provide the services for you!
This type of user will have priority over others when they need to store their items in other warehouses.

All the items stored in the warehouse will be based on this system: [_Loosed_ or _Anchored_](https://github.com/daniesnata/Olympus/blob/master/Zeus/RequestDoc-zeus-service-placement.md).

For tier _Basic_, _Standard_, and _Premium_, they can use either _Loosed_ or _Anchored_ system.

Tier ___Unicorn___ is an exception, as they own the whole ___Warehouse___ by itself.

