---
title: 'サンプル XML ファイル: 複数の購買発注書 - LINQ to XML'
description: (例で使用されている) この XML ファイルには、購買発注書に関するデータが含まれています。
ms.date: 07/20/2015
ms.assetid: 2d29fcaa-60df-43d4-8ccc-6cdba7c013e9
ms.openlocfilehash: ef50f8fe5558f6faa14f9c0c0261671d5c6e0b83
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "103412061"
---
# <a name="sample-xml-file-multiple-purchase-orders-linq-to-xml"></a><span data-ttu-id="4e359-103">サンプル XML ファイル : 複数の購買発注書 (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="4e359-103">Sample XML file: Multiple purchase orders (LINQ to XML)</span></span>

<span data-ttu-id="4e359-104">次の XML ファイルは、LINQ to XML ドキュメントのさまざまな例で使用されます。</span><span class="sxs-lookup"><span data-stu-id="4e359-104">The following XML file is used in various examples in the LINQ to XML documentation.</span></span> <span data-ttu-id="4e359-105">このファイルには、複数の購買発注書が含まれています。</span><span class="sxs-lookup"><span data-stu-id="4e359-105">This file contains several purchase orders.</span></span>

## <a name="purchaseordersxml"></a><span data-ttu-id="4e359-106">PurchaseOrders.xml</span><span class="sxs-lookup"><span data-stu-id="4e359-106">PurchaseOrders.xml</span></span>

```xml
<?xml version="1.0"?>
<PurchaseOrders>
  <PurchaseOrder PurchaseOrderNumber="99503" OrderDate="1999-10-20">
    <Address Type="Shipping">
      <Name>Ellen Adams</Name>
      <Street>123 Maple Street</Street>
      <City>Mill Valley</City>
      <State>CA</State>
      <Zip>10999</Zip>
      <Country>USA</Country>
    </Address>
    <Address Type="Billing">
      <Name>Tai Yee</Name>
      <Street>8 Oak Avenue</Street>
      <City>Old Town</City>
      <State>PA</State>
      <Zip>95819</Zip>
      <Country>USA</Country>
    </Address>
    <DeliveryNotes>Please leave packages in shed by driveway.</DeliveryNotes>
    <Items>
      <Item PartNumber="872-AA">
        <ProductName>Lawnmower</ProductName>
        <Quantity>1</Quantity>
        <USPrice>148.95</USPrice>
        <Comment>Confirm this is electric</Comment>
      </Item>
      <Item PartNumber="926-AA">
        <ProductName>Baby Monitor</ProductName>
        <Quantity>2</Quantity>
        <USPrice>39.98</USPrice>
        <ShipDate>1999-05-21</ShipDate>
      </Item>
    </Items>
  </PurchaseOrder>
  <PurchaseOrder PurchaseOrderNumber="99505" OrderDate="1999-10-22">
    <Address Type="Shipping">
      <Name>Cristian Osorio</Name>
      <Street>456 Main Street</Street>
      <City>Buffalo</City>
      <State>NY</State>
      <Zip>98112</Zip>
      <Country>USA</Country>
    </Address>
    <Address Type="Billing">
      <Name>Cristian Osorio</Name>
      <Street>456 Main Street</Street>
      <City>Buffalo</City>
      <State>NY</State>
      <Zip>98112</Zip>
      <Country>USA</Country>
    </Address>
    <DeliveryNotes>Please notify me before shipping.</DeliveryNotes>
    <Items>
      <Item PartNumber="456-NM">
        <ProductName>Power Supply</ProductName>
        <Quantity>1</Quantity>
        <USPrice>45.99</USPrice>
      </Item>
    </Items>
  </PurchaseOrder>
  <PurchaseOrder PurchaseOrderNumber="99504" OrderDate="1999-10-22">
    <Address Type="Shipping">
      <Name>Jessica Arnold</Name>
      <Street>4055 Madison Ave</Street>
      <City>Seattle</City>
      <State>WA</State>
      <Zip>98112</Zip>
      <Country>USA</Country>
    </Address>
    <Address Type="Billing">
      <Name>Jessica Arnold</Name>
      <Street>4055 Madison Ave</Street>
      <City>Buffalo</City>
      <State>NY</State>
      <Zip>98112</Zip>
      <Country>USA</Country>
    </Address>
    <Items>
      <Item PartNumber="898-AZ">
        <ProductName>Computer Keyboard</ProductName>
        <Quantity>1</Quantity>
        <USPrice>29.99</USPrice>
      </Item>
      <Item PartNumber="898-AM">
        <ProductName>Wireless Mouse</ProductName>
        <Quantity>1</Quantity>
        <USPrice>14.99</USPrice>
      </Item>
    </Items>
  </PurchaseOrder>
</PurchaseOrders>
```
