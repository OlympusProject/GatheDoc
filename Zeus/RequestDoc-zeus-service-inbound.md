# Inbound File Generation

This service should be developed under package ```com.zeus.service.inbound```

This service will generate ___InboundOrder___ and ___WarehouseInbound___ from a list of ___Product___ and their ___Stock___

## Definition
___InboundOrder___ is an order file to store new stocks to certain warehouses.

___WarehouseInbound___ is a subset of ___InboundOrder___ for one warehouse only.

A number of quantity of one ___Product___ which will be stored is a ___Stock___.

## Generation Process

The input of this process is a list of ___Product___ which will be stored to warehouses.

A ___Product___ can have ___Stock___ with certain quantity for one ___Warehouse___, and a ___Stock___ of another quantity to another ___Warehouse___.

A ___Stock___ can have a list of ___Stock___-___Warehouse___ pair, which the ___Stock___ act as stock with total quantity, and the ___Stock___-___Warehouse___ pair the subset for a certain ___Warehouse___.

The list of ___Product___ should be grouped into one inbound by which warehouse they're going to be stored. This grouped Products will be generated as ___WarehouseInbound___.

All ___WarehouseInbound___ must be persisted as one batch. If one ___WarehouseInbound___ is failed, the whole process should be rolled back.

Failed ___InboundOrder___ generation should be notified back to the caller services with good error message in XML or JSON format.

If new ___Product___ is added into the list (the product that isn't in DB), the ___Product___ need to be stored first, and only then it can proceed to generate the ___InboundOrder___ and ___WarehouseInbound___.

Note that if the dependencies of the ___Product___ -the ___Brand___; ___Category___; etc- hasn't exist yet, the ___Product___ can't be persisted. Send back error message.

If saving the new ___Product___ is failed, then fail the ___InboundOrder___ generation entirely.

The new ___Product___ can be more than one.

## After Generation

When the generation is completed, make PDF files for the ___InboundOrder___ and ___WarehouseInbound___.

The PDF generation is optional and can be enabled/disabled.

## Example


+ InboundOrder  
  DateTime 20180929T09:55:00  
  Code INODR20180929000001  
  Stocks qty 1550  

  Argan Oil 60ml - Stocks qty 600  
  to Warehouse KG - qty 200 bottles  
  to Warehouse PL - qty 250 bottles  
  to Warehouse GR - qty 150 bottles  

  Thyme 15ml - Stocks qty 500  
  to Warehouse KG - qty 100 bottles  
  to Warehouse SY - qty 400 bottles  

  Goat Milk Soap 110g - Stocks qty 250  
  to Warehouse SY - qty 75 pieces  
  to Warehouse PL - qty 25 pieces  
  to Warehouse GR - qty 100 pieces  
  to Warehouse KG - qty 50 pieces  

  Floating Lotus Conditioner - 345ml Stocks qty 200 (New Product)  
  to Warehouse PL - qty 150 bottles  
  to Warehouse GR - qty 50 bottles  



+ WarehouseInbound KG  
	Stocks qty 350  
	Argan Oil 60ml 200 bottles  
	Thyme 15ml 100 bottles  
	Goat Milk Soap 110g 50 pieces  


+ WarehouseInbound PL  
	Stocks qty 425  
	Argan Oil 60ml 250 bottles  
	Goat Milk Soap 110g 25 pieces  
	Floating Lotus Conditioner 150 bottles  


+ WarehouseInbound GR  
	Stocks qty 300  
	Argan Oil 60ml 150 bottles  
	Goat Milk Soap 110g 100 pieces  
	Floating Lotus Conditioner 50 bottles  


+ WarehouseInbound SY  
	Stocks qty 475  
	Thyme 15ml 400 bottles  
	Goat Milk Soap 110g 75 pieces  


